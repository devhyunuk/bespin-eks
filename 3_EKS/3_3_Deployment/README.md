# Deployment 배포

--- 
1. Deployment yaml 생성
```
cat <<EOF > deployment.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deploy
  template:
    metadata:
      labels:
        app: nginx-deploy
    spec:
      containers:
      - image: nginx
        name: nginx-container
EOF
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/b54db648-98d8-4009-9d63-296820fd884f)

2.  deployment.yaml 배포
```
kubectl apply -f deployment.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/4eaf8ebd-a5fc-4c90-831f-8915ada5cf97)

3. Deployment, ReplicaSet, Pod의 리스트를 확인
```
kubectl get deployment,replicaset,pods
또는
kubectl get deploy,rs,po
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/522d3f38-b1f8-43ac-ad85-a05c4f0e7dfd)

4. Kubernetes Object의 리스트와 짧은 이름, ApiVersion 등을 확인
```
kubectl api-resources
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/d9db361c-55d7-4baf-b8af-d08f001b8249)

5. ReplicaSet의 Pod의 개수를 모니터 (별도의 터미널을 하나 더 띄워서 아래 명령어를 실행)
```
kubectl get replicaset -w
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/037d1ae0-a2bc-4805-a09c-d63139f501ae)

6. deployment.yaml 파일을 열어서, image: nginx를 image: redis 로 변경한 후 저장 > 배포
```
kubectl apply -f deployment.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/5525aac7-d0dd-4b08-8bbc-1b86fba4bdee)

ReplicasSet의 Pod 들의 개수가 변경되는 걸 확인
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/a62fef1d-ab1d-442a-af96-dfed6dacc247)

이미지가 nginx > redis로 변경된 것 확인
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/126809f2-607d-4a6e-ac70-dc6c688842b1)


7. 배포된 것을 다시 롤백
```
kubectl rollout undo deploy nginx-deploy
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/fe7815c9-2334-4548-bc60-125e18383ac6)

이미지가 redis > nginx로 원복된 것 확인
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/98623968-27f4-4756-93d8-4cf4f2ee7798)
