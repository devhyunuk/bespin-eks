# ReplicaSet 배포

--- 
1. ReplicaSet yaml 생성
```
cat <<EOF > replicaset.yaml 
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-replicaset
  template:
    metadata:
      labels:
        app: nginx-replicaset
    spec:
      containers:
        - name: nginx-container
          image: nginx
EOF
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/accaf0d4-9bd8-4b97-a7a2-9daf3bb2e0b6)

2. replicaset.yaml을 배포
```
kubectl apply -f replicaset.yaml
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/09b5cda5-ac18-414e-a36a-c26c6c6c9a7a)


3. ReplicaSet과 Pod의 리스트를 확인
```
kubectl get replicaset,pods
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/e413e066-6c00-4afe-ae4f-e36696b0a94e)

4. 3개 중에 아무거나 하나의 Pod를 삭제
```
kubectl delete pod [pod 이름]
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/ceece13a-697b-4e31-97d8-91ea8cbc2bda)


5. ReplicaSet과 Pod의 리스트를 확인
```
kubectl get replicaset,pods
```

Pod이 하나 지워지고 새로운 Pod가 생겨난 걸 확인 (ReplicaSet이 Pod의 개수를 유지)
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/7e5e05ca-b1d6-4bcb-a749-95c1ebdc6107)


6. ReplicaSet의 Pod의 개수를 증가/감소 시킬수 있음
```
kubectl scale replicaset nginx-replicaset --replicas=5
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/6c04e90d-4a7e-411d-a830-97e3b117876f)

7. ReplicaSet과 Pod의 개수가 늘었는지 리스트를 확인
```
kubectl get replicaset,pods
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/20172b85-ff21-4ce8-8232-1a5e837fa83d)

8. ReplicaSet을 삭제
```
kubectl delete replicaset nginx-replicaset
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/90cd259d-537b-4fda-84e9-0b553c26dd86)


