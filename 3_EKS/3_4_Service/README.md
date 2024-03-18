# Service 배포

### 목표
- Service : LoadBalancer를 만들어서 Deployment를 Client에게 노출

--- 
1. ReplicaSet yaml 생성
```
cat <<EOF > 2048.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: game-2048
  labels:
    run: game-2048
spec:
  replicas: 3
  selector:
    matchLabels:
      app: game-2048
  template:
    metadata:
      labels:
        app: game-2048
    spec:
      containers:
      - image: public.ecr.aws/kishorj/docker-2048:latest
        name: game-2048
        ports:
          - containerPort: 80
            protocol: TCP
---
apiVersion: v1
kind: Service
metadata:
  name: "game-2048"
spec:
  type: LoadBalancer
  ports:
    - port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: game-2048
EOF
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/eae95d41-dbc7-4c9c-90b3-3b0918fd4022)

2. 2048.yaml을 배포 > 로드밸런서가 배포
```
kubectl apply -f 2048.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/714a220b-9b28-4c1a-94ce-a9ecaffe844b)

3. Deplyment와 Service의 리스트를 확인
- Service의 리스트에서 game-2048 의 EXTERNAL-IP 주소를 복사
- 브라우저에 붙여 넣으면 2048 게임이 실행되는 걸 확인
```
kubectl get deploy,svc
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/6b61b13b-0ea5-4353-ae7e-f29d3cee0a2b)
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/d0a378bb-2648-4419-be92-fb1e0449dc7b)

4. Deployment, Service yaml 파일을 기반으로 삭제
```
kubectl delete -f 2048.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/1eaaea43-c531-449a-8c2e-6403692f0343)
