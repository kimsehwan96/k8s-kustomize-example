# nginx simple

여러 k8s manifests 를 단순히 묶는 역할을 하는 예제. 

`$ kubectl kustomize . >> output.yaml` 



```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: nginx
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: nginx
spec:
  ports:
  - name: name-of-service-port
    port: 80
    protocol: TCP
    targetPort: http-web-svc
  selector:
    app.kubernetes.io/name: nginx
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: nginx-pdb
  namespace: nginx
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: nginx

```