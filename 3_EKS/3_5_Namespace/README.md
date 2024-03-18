# Namespace 배포

### 목표
- 클러스터를 논리적으로 부분 격리하는 Namespace 구

--- 
1. Namespace의 리스트를 확인
```
kubectl get namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/f115795c-aca2-48b4-8e13-491d85a5a6cb)

2. eks-namespace라는 이름으로 Namespace 생성
```
kubectl create namespace eks-namespace
```

3. 다음 명령어로 Namespace의 리스트를 확인합니다.
```
kubectl get namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/02cbb3f2-623f-48ed-9a1b-57b1d9cd6113)

4. eks-namespace에 nginx pod을 배포
```
kubectl run nginx --image=nginx -n eks-namespace
```

5. eks-namespace에 nginx pod이 배포되었는지 확인
```
kubectl get pod -n eks-namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/f39dc02c-64ba-4811-8337-af77ec2e6ed6)

6. eks-namespace를 삭제
```
kubectl delete namespace eks-namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/bc109551-ec54-49ca-b81d-873a9ebc014b)
네임스페이스가 삭제되면 pod도 삭제되는 것을 확인

7. 선언형으로 Namepsace를 만들어서 Pod을 배포
```
cat <<EOF > eks-namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: "eks-namespace"
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    run: nginx
  namespace: eks-namespace
spec:
  containers:
    - name: orange
      image: nginx
EOF
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/ccab8712-6c95-4bf5-a016-a81acaac3363)

8. Namepsace와 Pod를 배포
```
kubectl apply -f eks-namespace.yaml
```

9. eks-namespace에 nginx pod가 배포되었는지 확인
```
kubectl get pod -n eks-namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/22cbf136-2470-4d4e-a636-758fdd3d5192)

10. eks-namespace를 삭제
```
kubectl delete namespace eks-namespace
```
![image](https://github.com/devhyunuk/eks-essential/assets/49749510/977650ed-1974-4984-a6cd-0a62b73ed5c9)
