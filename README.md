# mobius_platform_docker
- 모비우스 플랫폼을 간편하게 도커로 실행할 수 있습니다
- `device-simulator`, `Mobius`, `Mosquitto`, `MySQL` 포함



## Mobius 프로젝트를 정상 실행하기 위한 수정 및 실행 절차 정리

### 수정해야 하는 파일 및 내용
- #### Mobius/conf.json (dbpass를 바꾸면 yml파일의 pw도 바꿔줘야 함)
    - 변경 전
        ```bash
        {
            "csebaseport": "7579",
            "dbpass": "bindsoft"   
        }
        ```
    - 변경 후
        ```bash
        {
            "csebaseport": "7579",
            "dbpass": "비밀번호 변경 값" <- docker-compose.yml의 `MYSQL_ROOT_PASSWORD` 값과 일치해야 함
        }
        ```
- #### Mobius/mobius.js - 37번 라인
    - 변경 전
        ```bash
        {
            global.usedbhost = 'localhost'
        }
        ```
    - 변경 후
        ```bash
        {
            global.usedbhost = 'db';  // docker-compose.yml 에 정의된 db 서비스명
        }
        ```
- #### Mobius/package.json - 11번 라인
    - 변경 전
        ```bash
        {
            "express": "^4.16.4",
        }
        ```
    - 변경 후
        ```bash
        {
            "express": "4.16.4",
        }
        ```
    - `^` 제거 이유 : 버전 업으로 인한 의존성 충돌 방지

### 서비스 실행
- `docker-compose.yml` 이 있는 디렉토리에서 실행
    
    ```bash
    docker-compose up -d
    ```

- 백그라운드에서 mobius, mysql 등의 서비스가 실행됩니다.