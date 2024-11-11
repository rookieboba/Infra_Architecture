# Infra_Architecture
Architect 설계

# 전사 서버 IT Infra 아키텍처

```
          +------------------------------------------+
          |                  인터넷                  |
          +------------------------+-----------------+
                                   |
                                   v
                      +------------------------+
                      |    로드 밸런서 (ALB)    |
                      +------------------------+
                                   |
             +---------------------+---------------------+
             |                                           |
             v                                           v
   +---------------------+                      +---------------------+
   |   웹 서버 (Web EC2)  | <-- Auto Scaling --> |   웹 서버 (Web EC2)  |
   +---------------------+                      +---------------------+
             |                                           |
             v                                           v
   +---------------------+                      +---------------------+
   |  애플리케이션 서버   |                      |  애플리케이션 서버   |
   |  (App EC2 - Multi-AZ) |                      |  (App EC2 - Multi-AZ) |
   +---------------------+                      +---------------------+
             |                                           |
             +---------------------+---------------------+
                                   |
                                   v
                        +---------------------+
                        |   DB 서버 (RDS)     |
                        |    Multi-AZ 설정    |
                        +---------------------+
                                   |
                                   v
                        +---------------------+
                        |   백업 및 복구 설정  |
                        | (EBS/RDS 스냅샷 등)  |
                        +---------------------+
                                   |
                                   v
                        +---------------------+
                        |    모니터링 및 로깅  |
                        | (CloudWatch 등)     |
                        +---------------------+
                                   |
                                   v
                        +---------------------+
                        |    보안 관리        |
                        | (IAM, 보안 그룹 등) |
                        +---------------------+
```

# 설명
- 위 아키텍처는 온프레미스와 클라우드 연동을 포함한 전사 IT 인프라 구성 예시입니다.
- Auto Scaling과 Multi-AZ 설정을 통해 가용성을 확보하고, 다양한 보안 및 백업 기능을 적용하였습니다.

# Terraform 사용
- 인프라를 배포하기 위해 다음과 같은 명령어를 단계적으로 사용하면 됩니다.

1. terraform.tfvars 파일 생성
```
bash create_tfvars.sh  
```

2. Terraform 초기화

```
terraform init
```
3. 계획 생성

```
terraform plan
```

4. 인프라 생성

```
terraform apply -auto-approve
```
