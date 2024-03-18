# EKS

### 목표
- EKS 설치
- kubectl 명령어
- Pod 배포
- ReplicaSet 배포
- Deployment 배포
- Service 배포
- Namespace 배포
- 리소스 삭제

--- 
### 1. EKS 설치
1. kubectl을 다운로드
```
sudo curl -o /usr/local/bin/kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.26.4/2023-05-11/bin/linux/amd64/kubectl
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/5b6db9fb-b209-4738-98df-b197bfb0e8f8)

2. 실행 권한 추가
```
sudo chmod +x /usr/local/bin/kubectl
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/5460b8c7-09dd-46ff-9c6b-e120944bb67d)

3. kubectl 버전 확인
```
kubectl version --client=true --short=true
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/476ba2a2-73e0-45d5-a5d9-0f303d9b652a)

4.  eksctl을 다운로드하고 압축 풀기
```
curl --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/c5aa6d14-3ef4-4f87-a0fb-7b7d36c2a67e)

5. eksctl을 /usr/local/bin 디렉터리로 이동 (전역에서 실행 가능 하도록)
```
sudo mv -v /tmp/eksctl /usr/local/bin
eksctl version
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/743b7ff5-1704-4ab7-9a39-218d4f42f50f)

6. 현재 리전의 정보를 환경변수에 저장
```
export AWS_REGION=$(curl --silent http://169.254.169.254/latest/meta-data/placement/region) && echo $AWS_REGION
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/d82717a9-36ce-43b9-9897-94f0bee0ab44)

7. eks를 배포 (약 15분 정도 소요)
```
eksctl create cluster --name myeks --version 1.26 --region ${AWS_REGION}
```
![image](https://github.com/devhyunuk/bespin-essential/assets/49749510/b10d697a-b42a-4f2f-9e07-1c8233461c06)

8. 노드의 리스트를 확인
```
kubectl get nodes
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/556fe236-cef7-4b5f-b5de-47b019be0ef8)


--- 
### 2. 리소스 삭제
1. EKS 삭제
```
eksctl delete cluster --name myeks --region ${AWS_REGION}
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/0d6f74d8-8e41-45cf-8848-facf4b56477d)

2. Cloud9 인스턴스 삭제
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/9e0c1dd6-e7ae-4aa6-9acc-02d9a6d09983)

3. IAM 에서 admin eksrole 삭제

4. Elastic Container Registry 에서 리포지토리 삭제


























