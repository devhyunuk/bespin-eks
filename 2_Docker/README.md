# Cloud9 IDE 환경 구성

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
1. 









--- 
### 2. 인증/자격증명 및 환경 구성
#### 1. IAM을 활용하여 역할(Role) 만들어서 권한 부여하는 방법

















