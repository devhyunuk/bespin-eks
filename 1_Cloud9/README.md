# Cloud9 IDE 환경 구성



### 목표
- Docker를 사용하여 컨테이너 이미지를 생성하고 배포하는 방법을 익히는 것
- 컨테이너 개수가 많아지게 되면 이를 효율적으로 다루는 방법을 배우는 것
- EKS를 사용하여 컨테이너를 효율적으로 관리하는 방법을 익히는 것

--- 
### 1. Cloud9 생성
1. 환경 생성(Create environment) 버튼 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/1e6f21a2-d351-4e1c-8643-cb303fd99ce4)

2. 이름(Name)에 hyunuk-cloud9를 입력
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/6438ee0a-63c1-43ac-aee6-81a46cc54766)

3. 인스턴스 유형에 t3.small을 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/04f8ba66-7012-47d4-a4e4-d63c37b7207b)

4. 생성(Create) 버튼 클릭
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/f52bd284-d5f7-43e8-b688-053878291a64)

5. 열림(Open) 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/29eeecce-4b63-4ded-9cc8-c8c9ce636cb7)


--- 
### 2. 인증/자격증명 및 환경 구성
#### 1. IAM을 활용하여 역할(Role) 만들어서 권한 부여하는 방법

1. 역할(Role) 메뉴를 클릭하고, 역할 만들기(Create role) 버튼을 클릭합니다.
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/3967ff70-0ed7-4668-9ccc-f75b588a02c0)

2. AWS Service선택하고, EC2를 선택 (AWS 서비스에서 다른 서비스에 접근하기 위한 권한을 설정하기 위함)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/46a8ca39-882e-48a3-85b1-9710f126ede9)

3. AdministratorAccess 권한을 체크
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/fa886913-3df1-4401-92be-20017f93bbaa)

4. 역할 이름(Role name) 에 입력
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/82d3fdbd-f3db-4ce6-bab1-e4396f986333)

5. 역할 생성(Create role) 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/dfc47a69-625e-4349-8ee4-8b8fd0b34e30)

6. Cloud9 인스턴스를 선택 > 작업(Actions) 선택 > 보안(Security) 선택 > IAM 역할 수정(Modify IAM role) 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/499a9270-f8ec-4bf9-af11-37218c2c437b)

7. admin-eks-role 선택 > IAM 역할 업데이트(Update IAM role) 선택 > Cloud9 인스턴스에 AdministratorAccess권한 적용 완료
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/fdf1e370-28cc-4488-b698-999b9ed230fe)

8. 톱니바퀴 아이콘 선택 > AWS Settings 메뉴 선택 > AWS managed temporary credentials: 을 비활성화
   - 비활성화 사유 : AWS managed temporary credentials이 활성화 되어 있으면 Cloud9에서 수동으로 Credential을 수정하여도 적용되지 않고, temporary credentials 값으로 계속 유지 
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/9c16f63c-09ca-4432-b4d4-479ca638bf92)

9. 아래 명령어 실행 (기존에 존재하는 자격증명 파일을 제거)
```
rm -vf ${HOME}/.aws/credentials
```

10. Docker와 Kubernetes 관련 실습을 하기 위한 Cloud9을 만들고 권한 부여 완
