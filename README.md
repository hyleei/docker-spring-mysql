# 🐳 Docker Compose 프로젝트: Spring Boot + MySQL

이 프로젝트는 Docker Compose를 사용하여 Spring Boot 애플리케이션과 MySQL 데이터베이스를 설정하고 실행하는 방법을 보여줍니다.

## 🚀 프로젝트 구조

- `app/`: Spring Boot 애플리케이션 소스 코드
- `mysql/`: MySQL 관련 설정 및 초기화 스크립트
- `docker-compose.yml`: 전체 애플리케이션 스택 정의

## 🛠 설정 및 실행

1. **Docker Compose 실행**
   ```
   docker-compose up -d
   ```

2. **컨테이너 상태 확인**
   ```
   docker ps
   ```

3. **Spring Boot 애플리케이션 접속**
   - URL: `http://localhost:8088`

4. **MySQL 데이터베이스 관리**
   - 호스트: `localhost`
   - 포트: `3306`
   - 사용자: `root`
   - 비밀번호: (설정한 비밀번호)

## 📊 데이터베이스 관리

### MySQL 컨테이너 접속
```
docker exec -it mysqldb bash
```

### 데이터베이스 덤프 및 복원
1. 덤프 생성:
   ```
   mysqldump -u root -p fisa(기존DB이름) > fisadump.sql
   ```

2. 새 데이터베이스 생성:
   ```sql
   CREATE DATABASE newmysqldb;
   ```

3. 덤프 복원:
   ```
   mysql -u root -p newmysqldb < fisadump.sql
   ```
      ![image](https://github.com/user-attachments/assets/e9c3c38c-858a-4154-9f58-861bb0509603)

## 🔧 문제 해결

- 컨테이너 로그 확인: `docker logs [컨테이너ID 또는 이름]`
- 애플리케이션 재시작: `docker-compose restart`
