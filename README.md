# 테이블 정의서를 보고 설계한 최종 물리적 모델

## MySQL 실행

- `services.msc` 에서 MySQL 서비스 실행
- `cmd` 에서 `net start mysql` 명령어로 실행
- `cmd` 에서 `mysql -u root -p` 명령어로 접속
- `cmd` 에서 `mysql -u root -p < 파일명.sql` 명령어로 파일 실행

## MySQL Workbench 에서 설계

![image](https://github.com/user-attachments/assets/9dd9565a-e5cb-4dbd-98a0-3ecac5b6c6a9)
![image](https://github.com/user-attachments/assets/cd4e645f-0a40-4742-b66d-86bbc2f1ff89)
![image](https://github.com/user-attachments/assets/11acb7fb-7bf9-4900-af41-9ee66aef46e8)
![image](https://github.com/user-attachments/assets/b600ecfe-ca7f-4f5a-8010-febde8d2427f)
![image](https://github.com/user-attachments/assets/79d31c57-0be1-40f8-968b-5b568f1ee4ec)
![image](https://github.com/user-attachments/assets/3f4d7af7-2be9-4617-8a3a-58a4229ce846)

- **CREATE DATABASE study;**
  - semicolon 을 붙여야 한다.

```sql
CREATE DATABASE study;
```

- schema 탭을 선택해야 한다.

![image](https://github.com/user-attachments/assets/2ac4332c-d7a7-442c-a404-3249c19e9ec0)
![image](https://github.com/user-attachments/assets/283b52fe-1128-4977-a717-bbf13058a3fb)
![image](https://github.com/user-attachments/assets/f87e74dd-9cb8-4ea3-9cbe-cec0d8ef2269)

- 다이어그램을 그리기 위해서 Reverse Engineer 를 선택

![image](https://github.com/user-attachments/assets/bc0a3101-f710-4145-af1b-26b54577eaf8)

![image](https://github.com/user-attachments/assets/1cc461c5-6dd3-4ac2-bdaa-7dc2bf451424)

![image](https://github.com/user-attachments/assets/28578b93-a92f-49b9-a3ed-0ad731291dba)

- 어떤 DB 를 그릴지 선택

![image](https://github.com/user-attachments/assets/8a32105a-ef9c-49e0-9ad0-adc218a3459f)

![image](https://github.com/user-attachments/assets/563377a5-264f-47d3-b39e-1c7b1da0622e)

![image](https://github.com/user-attachments/assets/8f05bf4d-f807-48ee-8dfd-443e8500230c)

![image](https://github.com/user-attachments/assets/35679672-5ec1-470e-9a24-2c20277aaa7f)

![image](https://github.com/user-attachments/assets/370bb646-1af1-444a-b2e3-1eec3fdeadf9)

![image](https://github.com/user-attachments/assets/d1d835e9-1fbe-4444-a7f6-2b8cdc3b86da)

- 자동으로 나온다.

## 작성순서

- 참조를 해야 하므로 지역 부터 작성
