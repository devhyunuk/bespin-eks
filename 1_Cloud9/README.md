# Cloud9 IDE 환경 구성



### 목표
- Docker를 사용하여 컨테이너 이미지를 생성하고 배포하는 방법을 익히는 것
- 컨테이너 개수가 많아지게 되면 이를 효율적으로 다루는 방법을 배우는 것
- EKS를 사용하여 컨테이너를 효율적으로 관리하는 방법을 익히는 것

--- 
### 1. Cloud9 생성
1. 환경 생성(Create environment) 버튼 선택
![img.png](img.png)

2. 이름(Name)에 hyunuk-cloud9를 입력
![img_1.png](img_1.png)

3. 인스턴스 유형에 t3.small을 선택
![img_2.png](img_2.png)

4. 생성(Create) 버튼 클릭
![img_3.png](img_3.png)

5. 열림(Open) 선택
![img_4.png](img_4.png)


--- 
### 2. 인증/자격증명 및 환경 구성
#### 1. IAM을 활용하여 역할(Role) 만들어서 권한 부여하는 방법

1. 역할(Role) 메뉴를 클릭하고, 역할 만들기(Create role) 버튼을 클릭합니다.
![img_6.png](img_6.png)

2. AWS Service선택하고, EC2를 선택 (AWS 서비스에서 다른 서비스에 접근하기 위한 권한을 설정하기 위함)
![img_5.png](img_5.png)

3. AdministratorAccess 권한을 체크
![img_7.png](img_7.png)

4, 역할 이름(Role name) 에 입력
![img_8.png](img_8.png)

5. 역할 생성(Create role) 선택
![img_9.png](img_9.png)

6. Cloud9 인스턴스를 선택 > 작업(Actions) 선택 > 보안(Security) 선택 > IAM 역할 수정(Modify IAM role) 선택
![img_10.png](img_10.png)
7. 






