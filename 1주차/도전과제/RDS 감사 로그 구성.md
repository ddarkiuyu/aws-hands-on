### [RDS]
#### Amazon RDS MySQL 생성
 - <https://catalog.workshops.aws/general-immersionday/ko-KR/advanced-modules/database/create-rds>

#### Audit 플러그인 활성화
- Option 그룹 생성
- <https://aws.amazon.com/ko/blogs/korea/configuring-an-audit-log-to-capture-database-activities-for-amazon-rds-for-mysql-and-amazon-aurora-with-mysql-compatibility/>
```
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

- 단일 이벤트에 대한 감사 활성화
```
1. Amazon RDS 콘솔에서 “Parameter groups”을 선택합니다.
2. 원하는 파라미터 그룹을 선택합니다.
3. “Parameters”에서 값으로 QUERY_DML을 선택합니다.
4. “Save changes”를 선택해 변경 사항 저장합니다.

※ 참고
CONNECT – Connection 성공, Connection 실패, 그리고 disconnections에 대한 로그. 이 값에는 사용자 정보가 포함됩니다.
QUERY – 구문 또는 권한 오류로 인해 실패한 쿼리를 포함하여 모든 쿼리 텍스트 및 쿼리 결과를 일반 텍스트로 기록합니다.
QUERY_DCL – QUERY와 유사하지만 DCL 타입 쿼리 (GRANT, REVOKE 등) 만 반환합니다.
QUERY_DDL – Query와 유사하지만 DDL 타입 쿼리 (CREATE, ALTER 등) 만 반환합니다.
QUERY_DML – Query와 유사하지만 DML 타입 쿼리 (INSERT, UPDATE 등) 만 반환합니다.
TABLE – 쿼리 실행의 영향을받은 테이블을 기록합니다. 이 옵션은 Amazon Aurora MySQL에 대한 고급 감사에서만 지원됩니다.
```

#### Option 그룹 정책 적용
- RDS Databases > Modify > Log exports에서 Audit log 체크(CloudWatch Log Groups에서 확인을 위한 설정)


#### 활성화된 Audit 로그 확인 및 다운로드
- CloudWatch > Logs > Log groups > /aws/rds/instance/'database명'/audit
- Actions > Exports results > Download search results(CSV)
