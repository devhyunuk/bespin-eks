# Pod 명령어

--- 
1. Pod 명령어 배포
```
kubectl run nginx-apple --image=nginx

[설명]
- kubectl: 쿠버네티스에 명령어를 보내는 유틸리티
- run: 실행 명령어
- nginx-apple: Pod의 이름
- --image=nginx: nginx 컨테이너 이미지를 사용
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/47d89db2-611d-46b7-8fec-691fdfaf5a23)


2. Pod의 리스트 확인
```
kubectl get pods
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/33e92fdd-f846-4e7f-8039-d70bb0742f9c)


3. Pod 선언형(yaml) 배포 (선언형(yaml)파일 생성)
```
cat <<EOF > nginx-orange.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: nginx-orange
  labels:
    run: nginx-orange
spec:
  containers:
    - name: orange
      image: nginx
EOF
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/f4c0f352-27e1-4b8f-bd4a-10c8fadf5bcc)


4. yaml 파일을 배포하여 Pod을 생성
```
kubectl apply -f nginx-orange.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/5e407348-d37a-41d2-a5eb-69d986eb7438)

5. Pod가 어느 노드에 배포되었는지 확인
```
kubectl get pods -o wide
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/4bccc47c-eea0-4d64-8b28-0834adb71945)

6. Pod의 레이블을 확인
```
kubectl get pods --show-labels
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/bbd7a080-7fd5-47ce-9c2d-fbca2e533344)

7. Pod을 삭제 명령어
```
kubectl delete pods nginx-apple
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/f84de2c1-abf3-4887-972b-9614bb82b6a6)


8. 특정 레이블의 Pod을 삭제
```
kubectl delete pods -l run=nginx-orange
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/7804bba9-8ce2-4b1a-9427-dd385b6e3081)
