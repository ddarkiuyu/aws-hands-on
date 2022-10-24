## 목표
* AWS Lambda와 Amazon SNS, Amazon EventBridge를 활용하여, 스케줄링을 통한 SMS 발송하기

참조 URL:
 - https://docs.aws.amazon.com/ko_kr/iot/latest/developerguide/iot-lambda-rule.html#iot-lambda-rule-create-lambda

## 세부 내용
### 1단계: AWS IAM 설정
> IAM 접속 → Roles → Create role → Use case: Lambda 선택 후 Next → AmazonSNSFullAccess 검색 후 체크 선택 후 Next → Role name: role_send_sms 후 Create role 

### 2단계: AWS Lambda 설정
> 
