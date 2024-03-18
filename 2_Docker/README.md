<img width="549" alt="image" src="https://github.com/devhyunuk/bespin-essential/assets/49749510/a64e8723-8e32-4d6d-8353-47393eea4b7e"># Cloud9 IDE 환경 구성

### 목표
- Docker 명령어
- Docker image build
- Docker Repository에 image upload
- Docker Volume (저장 공간)
- Docker Network
- 멀티 컨테이너 애플리케이션
- Docker compose

--- 
### 1. Docker 명령어
1. nginx(웹서버) Docker 이미지를 검색
```
docker search nginx
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/fece8a60-e8fe-4eff-9a94-2068657ab3ec)


2. 가장 다운로드 수가 많은 공식 nginx 이미지를 다운로드
```
docker pull nginx
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/c6391e77-4df1-4241-9f66-3fd297141a7f)


3. Docker 이미지 다운로드 됐는지 확인
```
docker images
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/3e82f340-b9d5-43b5-b075-4440d80efcc1)


4. nginx 이미지를 기반으로 컨테이너를 실행 > 브라우저에 Cloud9 인스턴스의 Public IP 주소를 입력하여 "Welcome to nginx!" 화면이 제대로 나오는지 확인
```
docker run --name nginx-test -d -p 80:80 nginx

—-name: 컨테이너의 이름 지정(생략 : 랜덤하게 이름 생성)
-d: 백그라운드에서 실행
-p 80:80: 앞에 80번 포트로 접근하면 컨테이너의 80번 포트로 연결하라는 포트 매핑하는 옵션
nginx는 풀(다운)받을 이미지 이름
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/800b6861-bb12-4d98-8d92-f540d526fa6e)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/fcc60387-1db2-4898-8cff-0dc05d3e7e94)

5. 실행되고 있는 컨테이너를 확인
```
docker ps
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/7f3c5c06-3e65-4cc3-8d41-5dde0391edc6)

6. 실행되고 있는 컨테이너를 정지
```
docker stop nginx-test
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/c123c646-fd4b-4e18-8622-e2c1c77bfc85)

7. 모든(실행되고 있는, 정지된) 컨테이너를 확인 (정지된 nginx-test 컨테이너 확인)
```
docker ps -a
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/d4ace7b6-0ad3-4760-9ae9-f8ed32c73519)

8. 정지된 컨테이너 다시 실행
```
docker start nginx-test
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/bd19cb97-f469-464d-8306-5557b9d0592c)

9. 2000번 포트로 nginx-orange 컨테이너를 하나 더 실행 > 브라우저에 Cloud9 인스턴스의 Public IP:2000 주소를 입력하여 "Welcome to nginx!" 화면이 제대로 나오는지 확인
```
docker run --name nginx-orange -d -p 2000:80 nginx
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/3be4c1ea-2d8c-4ec6-93d8-7e51289e84e9)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/29096338-37be-4d5e-b5f8-e89e1cee1edf)

10. 실행 중인 컨테이너를 확인 > 2개의 컨테이너가 실행되고 있는 걸 확인
```
docker ps
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/6a62c1e0-ab70-4d29-acd3-9d2c7096d27f)

11. 컨테이너 삭제 시도 > 에러 발생 > 컨테이너가 실행 중이기 때문에 지울 수가 없음
```
docker rm nginx-test
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/253b697a-30f3-4b80-a8cd-7e117c4e3411)

12. 컨테이너 정지
```
docker stop nginx-test
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/97bf4223-ae9a-418a-b8f8-2988dbefa189)

13. 실행 중인 또는 정지된 모든 컨테이너를 확인
```
docker ps -a
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/b8c2a035-691c-4b2e-ac4e-b4a7c19ca4eb)

14. 정지된 nginx-test 컨테이너를 삭제
```
docker rm nginx-test
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/330b944b-366c-4e9c-8f6a-106d92153f7b)

15. 이미지 삭제 시도 > 에러 발생 > nginx 이미지를 nginx-orange 컨테이너가 사용하고 있기 때문에 지울 수가 없음
```
docker rmi nginx
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/21aad51e-f676-4f00-8e4d-92aa8b440384)

16. nginx-orange 컨테이너를 정지 > 컨테이너 삭제 > 이미지 삭제
```
docker stop nginx-orange
docker rm nginx-orange
docker rmi nginx
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/ac4321db-2095-4e5c-93b8-752bec1b298c)


--- 
### 2. Docker image build
1. 깃허브에 오픈되어 있는 2048게임 코드를 다운
```
git clone https://github.com/gabrielecirulli/2048
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/d70d7d81-2e55-4527-9ca4-ec7d4b286b77)

2. 다운받은 2048게 디렉토리로 이동
```
cd ~/environment/2048
```

3. Dockerfile 생성 명령어
```
cat <<EOF > Dockerfile 
FROM nginx:latest

COPY . /usr/share/nginx/html

EXPOSE 80
EOF
```

4. Docker 이미지 다운로드 확인
```
docker build -t game2048 .
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/2c2904a1-2eeb-4339-95bc-afb3ce969849)

5. Docker 이미지를 기반으로 컨테이너를 실행 > 브라우저에 Cloud9 인스턴스의 Public IP 주소를 입력하여 2048 게임 화면이 제대로 나오는지 확인
```
docker run --name game2048 -dp 80:80 game2048
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/bd45f758-9953-4f6a-b04f-7de9b0f48da3)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/a34b144f-f52a-4f6e-b074-59f9b055871b)

6. 모든 컨테이너를 삭제 > 모든 이미지 삭제
```
docker rm -f $(docker ps -aq)
docker rmi -f $(docker images -q)
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/d5b3c6d0-7b25-4ffb-8607-aa60c3d32b9c)

--- 
### 3. ECR에 Docker image upload
1. ECR 레포지토리 만들기 > Elastic Container Registry 이동 > 리포지토리 생성(Create repository) 버튼 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/73e62bc1-1130-4f86-b2c9-b8d9b33ad4b4)

2. 리포지토리 이름(Repository name) 에 hyunuk-repo를 입력
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/08e4d8bc-5ea3-41de-ae45-0c1b1abebe1a)

3. 리포지토리 생성(Create repository) 버튼 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/7f6d743a-f3a0-4a2a-8614-8ed3e513ed61)

4. hyunuk-repo 선택 > 푸시 명령 보기(View push commands) 버튼 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/92c9864f-4afb-49dc-b6d8-4383d98429b8)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/ad2df80a-8830-43f4-96a6-a39b1f1e10ab)

5. 리포지토리(Repository) 에 인증하는 명령어, 이미지 빌드, 태깅, 푸쉬(업로드) 하는 명령어 확인
<img width="411" alt="image" src="https://github.com/devhyunuk/bespin-essential/assets/49749510/edc790a3-05f5-444f-a603-8b5e40412347">

6. 푸시 명령어 중에 1번, 인증하는 명령어를 복사하여 Cloud9 의 터미널창에 실행
<img width="549" alt="image" src="https://github.com/devhyunuk/bespin-essential/assets/49749510/eff35c5b-f850-48f6-b02e-5aa7531d0540">

7. 푸시 명령어 중에 2번, 이미지 빌드하는 명령어 실행
```
docker build -t hyunuk-repo .
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/3c9cb6b1-60cb-4e90-8101-7cc55aadb6e8)

8. 푸시 명령어 중에 3번 명령어를 실행하여 이미지를 태깅
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/007526c9-8240-4ec4-b74e-8642f09983cf)

9. 이미지가 잘 태깅이 됐는지 확인 > hyunuk-repo 이미지가 새로운 308943070041.dkr.ecr.ap-northeast-1.amazonaws.com/hyunuk-repo 이름으로 태깅이 된 것을 확인
```
docker images
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/945afa9f-7552-4887-b9bb-0fd29f11b7fe)

10. 푸시 명령어 중에 4번 명령어를 실행하여 이미지를 리포지토리(Repository) 에 푸쉬
```
docker push 308943070041.dkr.ecr.ap-northeast-1.amazonaws.com/hyunuk-repo:latest
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/d035826e-2e3b-4c24-8001-57fa51ac37f9)

11. 푸시한 이미지 확인 > 이미지 태그인 latest를 선택
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/33ebc23f-ad6d-47be-9351-9f39209a54fe)

12. URI가 이미지 주소 > URI를 통해 실행
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/4067cfed-7b2c-4478-b8d2-9d690c356c09)

13. 모든 컨테이너 이미지를 삭제
```
docker rmi -f $(docker images -q)
```

14. ECR Repository에서 이미지를 풀(다운) 받아서 실행
```
docker run --name 2048 -dp 2000:80 308943070041.dkr.ecr.ap-northeast-1.amazonaws.com/hyunuk-repo:latest
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/f55edd32-c8e7-469e-8a65-dc62678d76f4)
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/c7b6f3eb-d085-4ad7-8369-91827477c028)



































