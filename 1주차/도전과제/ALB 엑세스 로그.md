## 세부내용
### [ALB]
#### 로그 저장을 위한 S3 버킷 생성 및 권한 설정
- S3 버킷 생성(ALB와 동일 리전 / 버킷 생성 네이밍 규칙 확인)
```
create bucket  → 버킷 이름 설정 → AWS 리전 선택(시드니)
public access 설정에서 Block all public access 체크해제 → 아래 경고창 체크 후 버킷 생성
```

- 새로운 버킷 정책 생성(ALB에서 S3 저장을 위한 정책 설정)
```
생성된 버킷 선택 후 permission 선택
아래 버킷 정책에 아래 JSON 파일 입력
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::783225319266:root"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::web-yk53-lab/alb_log/AWSLogs/035135759817/*"
        },
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::web-yk53-lab/alb_log/AWSLogs/035135759817/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        },
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:GetBucketAcl",
            "Resource": "arn:aws:s3:::web-yk53-lab"
        }
    ]
}
```
<img src="https://drive.google.com/file/d/1084MTBXY-UnUSJUe7NsNpS1uZHCFdTDE/view?usp=sharing" width="600px" height="400px" title="px(픽셀) 크기 설정" alt="Bucket Policy"></img><br/>

#### ALB 엑세스 로그 활성화
- General Immersion Day Workshop > 심화모듈 - 웹어플리케이션 > 컴퓨트 - Amazon EC2에 생성한 Web-ALB에 대하여, 엑세스 로그 활성화
```
EC2 → Load Balancers → 생성한 로드밸런서 선택 후 아래쪽으로 내려보면 edit attributte 클릭
Access logs Enable 체크
S3 location: s3://web-yk53-lab/alb_log
```

#### ALB 테스트 및 S3내 엑세스 로그 파일 확인 및 다운로드
- ALB 접속 테스트를 통하여 로그 생성후, 해당 로그 파일 다운로드
```
http://web-alb-751714237.ap-southeast-2.elb.amazonaws.com/ 접속 후 F5 2~3번 수행
Amazon S3 > Buckets > web-yk53-lab > alb_log/ > AWSLogs/ > 035135759817/ > elasticloadbalancing/ > ap-southeast-2/ > 2022/ > 10/ > 19/ 로그확인
s3://web-yk53-lab/alb_log/AWSLogs/035135759817/elasticloadbalancing/ap-southeast-2/2022/10/19/035135759817_elasticloadbalancing_ap-southeast-2_app.Web-ALB.3ed6c5952acfe2d7_20221019T0545Z_13.236.99.216_3n9llmor.log.gz
```
