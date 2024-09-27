# 🐳 Docker Compose 프로젝트: Spring Boot + MySQL + Cron

이 프로젝트는 Docker Compose를 사용하여 Spring Boot 애플리케이션, MySQL 데이터베이스, 그리고 Cron 작업을 포함한 통합 환경을 설정하고 실행하는 방법을 보여줍니다.

## 🚀 프로젝트 구조

- `app/`: Spring Boot 애플리케이션 소스 코드
- `mysql/`: MySQL 관련 설정
- `cron/`: Cron 작업 관련 파일
  - `Dockerfile`: Cron 서비스를 위한 Docker 이미지 정의
  - `crontab`: Cron 작업 스케줄 정의
  - `scripts/`: Cron 작업 스크립트 (예: backup.sh)
- `docker-compose.yml`: 전체 애플리케이션 스택 정의

## 🛠 설정 및 실행

1. **Docker Compose 실행**
   ```
   docker-compose up -d
   ```

2. **컨테이너 상태 확인**
   ```
   docker-compose ps
   ```

3. **Spring Boot 애플리케이션 접속**
   - URL: `http://localhost:8088`

4. **MySQL 데이터베이스 관리**
   - 호스트: `localhost`
   - 포트: `3306`
   - 사용자: `root`
   - 비밀번호: `root`
   - 데이터베이스: `fisa`

## 📊 데이터베이스 관리

### MySQL 컨테이너 접속
```
docker exec -it mysqldb bash
```

### 데이터베이스 접속
컨테이너 내부에서:
```
mysql -u root -p
```
비밀번호 입력 후 MySQL 프롬프트에 접속할 수 있습니다.

## 📂 볼륨 관리

이 프로젝트는 Docker 볼륨을 사용하여 데이터의 영속성을 보장합니다.

- `mysql_data`: MySQL 데이터베이스 파일 저장
- `app_logs`: 애플리케이션 로그 파일 저장

볼륨 목록 확인:
```
docker volume ls
```
![image](https://github.com/user-attachments/assets/f7e15cc3-bfd3-46d5-9836-06bfefd51145)


## ⏱ 크론 작업

주기적인 작업을 위해 크론 서비스를 사용합니다.

### 크론 설정 확인
```
docker exec step06compose-cron-1 crontab -l
```
![image](https://github.com/user-attachments/assets/462a2485-71fb-466f-96b4-4483a595c11c)


### 백업 스크립트 수동 실행
```
docker exec step06compose-cron-1 /scripts/backup.sh
```

### 크론 로그 확인
```
docker-compose logs cron
```

### 백업 파일 확인
```
docker exec mysqldb ls /var/lib/mysql
```
![image](https://github.com/user-attachments/assets/ed56af51-6a32-41b0-a7b9-262113336fd4)

또는
```
docker exec mysqldb find / -name "fisa_backup_*.sql"
```
![image](https://github.com/user-attachments/assets/351be903-d3d6-48e9-96db-ad50eda5fd3a)

## 🔧 문제 해결

1. **컨테이너 로그 확인**
   ```
   docker-compose logs [서비스명]
   ```
   예: `docker-compose logs app` 또는 `docker-compose logs db`

2. **애플리케이션 재시작**
   ```
   docker-compose restart
   ```

3. **전체 서비스 재시작**
   ```
   docker-compose down
   docker-compose up -d
   ```

4. **백업 스크립트 내용 확인**
   ```
   docker exec step06compose-cron-1 cat /scripts/backup.sh
   ```
   ![image](https://github.com/user-attachments/assets/27c2f720-476d-48d7-be29-e3a7a8c5aaac)


5. **크론 설정 수정 (필요시)**
   - `cron/crontab` 파일 수정 후:
     ```
     docker-compose up -d --build cron
     ```

6. **볼륨 데이터 확인**
   ```
   docker volume inspect [볼륨_이름]
   ```
   ![image](https://github.com/user-attachments/assets/23bb5e12-16cc-4ee5-8981-a0f24caba871)
   ![image](https://github.com/user-attachments/assets/fbf7e75a-f69d-42b0-8e66-86d9bc6e6434)


