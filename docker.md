# PackitCinema Docker 컨테이너화

기존에 호스트에서 직접 돌아가던 PHP + MariaDB 웹 애플리케이션(PackitCinema)을
Docker Compose로 컨테이너화한 실습 프로젝트입니다.

## 📊 구조

```
브라우저
   ↓
http://<서버IP>:8080
   ↓
Docker Container (PHP 8.1 + Apache)
   ↓ (Docker 내부 네트워크)
Docker Container (MariaDB)
```

## 🛠 사용 기술

- Docker / Docker Compose
- PHP 8.1 (Apache)
- MariaDB

## 📁 프로젝트 구성

```
/var/www/html
├── Dockerfile
├── docker-compose.yml
└── packitcinema/        # PHP 소스코드 (기존 웹 애플리케이션)
    └── config.php
```

## 1. Dockerfile

PHP 8.1 + Apache 기반 웹 서버 이미지를 정의합니다.

```dockerfile
FROM php:8.1-apache
RUN a2enmod rewrite
RUN docker-php-ext-install pdo pdo_mysql
WORKDIR /var/www/html
RUN chown -R www-data:www-data /var/www/html
EXPOSE 80
CMD ["apache2-foreground"]
```

## 2. docker-compose.yml

`web`(PHP/Apache)과 `db`(MariaDB) 두 개의 서비스를 정의하고,
Docker가 자동으로 만들어주는 내부 네트워크로 서로 통신하게 합니다.

```yaml
services:
  web:
    build: .
    container_name: packitcinema_web
    ports:
      - "8080:80"
    volumes:
      - ./packitcinema:/var/www/html/packitcinema
    depends_on:
      - db
    environment:
      - TZ=Asia/Seoul
    restart: unless-stopped

  db:
    image: mariadb:latest
    container_name: packitcinema_db
    environment:
      MYSQL_ROOT_PASSWORD: rootpass123!
      MYSQL_DATABASE: packitcinema
      MYSQL_USER: cinemauser
      MYSQL_PASSWORD: cinema123!
    volumes:
      - db_data:/var/lib/mysql
    restart: unless-stopped

volumes:
  db_data:
```

> `db` 서비스에는 호스트 포트를 별도로 열지 않았습니다. `web` 컨테이너는
> Docker 내부 네트워크에서 `db`라는 이름(서비스명)으로 MariaDB에 접근합니다.

## 3. config.php 수정

기존에는 `localhost`로 DB에 접속했지만, 컨테이너 환경에서는 DB 컨테이너의
**서비스명(`db`)**을 호스트로 사용해야 합니다.

```php
<?php
session_start();
$DB_HOST = 'db';
$DB_NAME = 'packitcinema';
$DB_USER = 'cinemauser';
$DB_PASS = 'cinema123!';
try {
    $pdo = new PDO("mysql:host={$DB_HOST};dbname={$DB_NAME};charset=utf8mb4", $DB_USER, $DB_PASS, [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    ]);
} catch (PDOException $e) {
    die('DB 연결 실패: ' . htmlspecialchars($e->getMessage()));
}
function e($value) {
    return htmlspecialchars((string)$value, ENT_QUOTES, 'UTF-8');
}
function is_login() {
    return isset($_SESSION['user']);
}
function is_admin() {
    return isset($_SESSION['user']) && (int)$_SESSION['user']['is_admin'] === 1;
}
function require_login() {
    if (!is_login()) {
        header('Location: login.php');
        exit;
    }
}
function require_admin() {
    require_login();
    if (!is_admin()) {
        security_log('ADMIN_DENIED', '관리자 페이지 접근 차단');
        http_response_code(403);
        die('관리자만 접근할 수 있습니다.');
    }
}
function client_ip() {
    return $_SERVER['REMOTE_ADDR'] ?? 'unknown';
}
function security_log($event, $message = '') {
    $dir = __DIR__ . '/logs';
    if (!is_dir($dir)) mkdir($dir, 0775, true);
    $line = sprintf("[%s] ip=%s user=%s event=%s msg=%s\n",
        date('Y-m-d H:i:s'),
        client_ip(),
        $_SESSION['user']['username'] ?? '-',
        $event,
        str_replace(["\r", "\n"], ' ', $message)
    );
    file_put_contents($dir . '/security.log', $line, FILE_APPEND);
    error_log("PACKITCINEMA {$event} {$message}");
}
function current_user_id() {
    return $_SESSION['user']['id'] ?? null;
}

```

## 4. 컨테이너 실행

```bash
cd /var/www/html
sudo docker compose up -d
sudo docker compose ps   # web, db 둘 다 Up 인지 확인
```

## 5. 기존 데이터 마이그레이션 (호스트 → 컨테이너)

기존에 호스트에서 직접 운영하던 MariaDB의 데이터를 새 컨테이너 DB로 옮깁니다.

```bash
# 1) 호스트 DB 백업
sudo mysqldump -u root packitcinema > /tmp/backup.sql

# 2) 컨테이너 DB로 복구
sudo docker exec -i packitcinema_db mariadb -u cinemauser -pcinema123! packitcinema < /tmp/backup.sql

# 3) 확인
sudo docker exec packitcinema_db mariadb -u cinemauser -pcinema123! packitcinema -e "SHOW TABLES;"
```

정상적으로 `movies`, `notices`, `reservations`, `schedules`, `users` 테이블이
나오면 마이그레이션 성공입니다.

## ✅ 결과

- `http://<서버IP>:8080` 접속 시 기존과 동일한 영화관 사이트가 정상 동작
- 호스트 시스템과 완전히 격리된 환경에서 PHP + MariaDB 실행
- `docker compose up -d` / `down` 한 번으로 전체 애플리케이션 시작·종료 가능

## 📌 배운 점

- Docker Compose로 여러 컨테이너(웹 서버 + DB)를 함께 정의하고 실행하는 법
- 컨테이너 간 통신은 `localhost`가 아니라 **서비스명**으로 이루어진다는 점
- 기존 호스트 DB 데이터를 `mysqldump` / `docker exec`로 컨테이너에 이관하는 법
- 포트 매핑(`8080:80`)과 볼륨 마운트로 소스코드/데이터를 관리하는 법

## 🚀 다음에 해볼 것

- [ ] `.env` 파일로 비밀번호 등 환경변수 분리
- [ ] Docker Hub에 이미지 푸시
- [ ] GitHub Actions로 CI/CD 파이프라인 구성
- [ ] Kubernetes로 배포해보기
