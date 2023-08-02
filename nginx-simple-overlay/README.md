# nginx simple overlay

간단한 nginx manifests 들을 overlay (형상 별 분리)하여 생성하는 예제

이 예제는 patch 를 활용해 형상별 다른 설정값들을 지정 함

```text
.
├── README.md
├── base
│   ├── kustomization.yaml
│   ├── nginx-deployment.yaml
│   ├── nginx-namespace.yaml
│   ├── nginx-pdb.yaml
│   └── nginx-service.yaml
├── dev
│   ├── kustomization.yaml
│   ├── nginx-deployment-dev.yaml # patch
│   ├── nginx-service-dev.yaml # patch
│   └── output.yaml
└── prod
    ├── kustomization.yaml
    ├── nginx-deployment-prod.yaml # patch
    ├── nginx-service-prod.yaml # patch
    └── output.yaml

```

nginx-simple-overlay-2 디렉터리와 차이로는, base 에서 deployment, service, pdb 같은 모든 오브젝트를 base 에 정의하고, dev, prod 와 같은 overlay 디렉터리에서는 patch 할 부분에 대해서만 정의되었다는 것. 
## manifests(yaml) 생성

`$ kubectl kustomize --enable-helm . >> output.yaml` 

## install

`$ kubectl kustomize --enable-helm . | kubectl apply -f -` 
