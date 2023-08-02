# nginx simple overlay 2

간단한 nginx manifests 들을 overlay (형상 별 분리)하여 생성하는 예제

이 예제는 patch 를 쓰지 않고, 형상별 리소스를 따로 생성하여 분리함

```text
.
├── README.md
├── base
│   ├── kustomization.yaml
│   ├── nginx-namespace.yaml
│   └── nginx-pdb.yaml
├── dev
│   ├── kustomization.yaml
│   ├── nginx-deployment.yaml
│   ├── nginx-service.yaml
│   └── output.yaml
└── prod
    ├── kustomization.yaml
    ├── nginx-deployment.yaml
    ├── nginx-service.yaml
    └── output.yaml
```

nginx-simple-overlay 디렉터리와 차이로는, base 에서 deployment, service 같은 오브젝트를 정의하지 않았다는 것
## manifests(yaml) 생성

`$ kubectl kustomize --enable-helm . >> output.yaml` 

## install

`$ kubectl kustomize --enable-helm . | kubectl apply -f -` 
