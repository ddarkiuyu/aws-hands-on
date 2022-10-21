### [RDS]
#### Amazon RDS MySQL 생성
```
AWS General Immersion Day 데이터베이스 생성 참고
https://catalog.workshops.aws/general-immersionday/ko-KR/advanced-modules/database/create-rds
```

#### Audit 플러그인 활성화
- Option 그룹 생성
```
https://aws.amazon.com/ko/blogs/korea/configuring-an-audit-log-to-capture-database-activities-for-amazon-rds-for-mysql-and-amazon-aurora-with-mysql-compatibility/ 참조
1. Amazon RDS 콘솔에서 “Parameter groups”를 선택합니다.
2. “Create parameter group”을 선택합니다.
3. “Parameter group family”에서 aurora-mysql5.7을 선택합니다.
4. “Group name”에 이름을 입력합니다 (예 : aurora-db-cluster-57).
5. “Create”를 선택합니다.
이제 DB 클러스터 파라미터 그룹을 기존 Amazon RDS MySQL 인스턴스와 연결합니다.
6. Amazon RDS 콘솔에서, 인스턴스를 선택합니다.
7. “Action” 메뉴에서 “Modify”를 선택합니다.
8. “Additional configuration”의 “DB cluster parameter group” 항목에 이전에 생성 한 파라미터 그룹을 선택합니다.
9. “When to apply modifications”에서 “Immediately”를 선택하여, 다음 유지 관리 기간까지 기다리지 않도록합니다.
변경 사항을 적용하면 즉시 데이터베이스가 다시 시작됩니다.
10. “Modify cluster”를 선택합니다.
11. “Parameter groups” 페이지에서 파라미터 그룹을 선택합니다.
12. “Values”에 대해서,  매개 변수를 수정하여 고급 감사를 활성화하거나 비활성화합니다.
13. “Save changes”를 선택합니다.
```

#### Option 그룹 정책 적용
- RDS Databases > Modify > Log exports에서 Audit log 체크(CloudWatch Log Groups에서 확인을 위한 설정)


#### 활성화된 Audit 로그 확인 및 다운로드
- CloudWatch > Logs > Log groups > /aws/rds/instance/'database명'/audit
- Actions > Exports results > Download search results(CSV)
