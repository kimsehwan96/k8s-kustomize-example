# nginx simple patch

여러 k8s manifests 를 포함하고, patch 를 통해 레이블 및 특정 spec 정보를 변경하는 예제

`$ kubectl kustomize . >> output.yaml` 


```yaml
# add-label.patch.yaml:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app.kubernetes.io/version: 1.21.0
```

```yaml
# fix-version.patch.yaml:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: not-used
spec:
  template:
    spec:
      containers:
        - name: nginx
          image: nginx:1.21.0
```

```yaml
# kustomization.yaml
namespace: nginx

resources:
  - ./nginx-namespace.yaml
  - ./nginx-deployment.yaml
  - ./nginx-pdb.yaml
  - ./nginx-service.yaml

patches:
  - path: add-label.patch.yaml
  - path: fix-version.patch.yaml
    target:
      labelSelector: "app.kubernetes.io/name=nginx"
```

patches.target 을 지정하지 않을 경우 metadata.name, kind, apiVersion 을 통해 patch 할 리소스를 지정하고,

지정하는 경우에도 metadata.name 은 필수적으로 필요하지만, `target` 정보 기반으로 patch 할 리소스 지정

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
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
    app.kubernetes.io/version: 1.21.0
  name: nginx-deployment
  namespace: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx:1.21.0
        name: nginx
        ports:
        - containerPort: 80
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