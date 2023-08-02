# K8s kustomization example

## 구조

```text
.
├── README.md
├── argocd-helm
│   ├── README.md
│   ├── argocd-namespace.yaml
│   ├── kustomization.yaml
│   ├── output.yaml
│   ├── values.yaml
│   └── chart/ # 업스트림 helm chart 가 여기 저장됨. (template/, values.yaml 등)
├── nginx-simple
│   ├── README.md
│   ├── kustomization.yaml
│   ├── nginx-deployment.yaml
│   ├── nginx-namespace.yaml
│   ├── nginx-pdb.yaml
│   ├── nginx-service.yaml
│   └── output.yaml
├── nginx-simple-overlay
│   ├── README.md
│   ├── base
│   │   ├── kustomization.yaml
│   │   ├── nginx-deployment.yaml
│   │   ├── nginx-namespace.yaml
│   │   ├── nginx-pdb.yaml
│   │   └── nginx-service.yaml
│   ├── dev
│   │   ├── kustomization.yaml
│   │   ├── nginx-deployment-dev.yaml
│   │   ├── nginx-service-dev.yaml
│   │   └── output.yaml
│   └── prod
│       ├── kustomization.yaml
│       ├── nginx-deployment-prod.yaml
│       ├── nginx-service-prod.yaml
│       └── output.yaml
├── nginx-simple-overlay-2
│   ├── README.md
│   ├── base
│   │   ├── kustomization.yaml
│   │   ├── nginx-namespace.yaml
│   │   └── nginx-pdb.yaml
│   ├── dev
│   │   ├── kustomization.yaml
│   │   ├── nginx-deployment.yaml
│   │   ├── nginx-service.yaml
│   │   └── output.yaml
│   └── prod
│       ├── kustomization.yaml
│       ├── nginx-deployment.yaml
│       ├── nginx-service.yaml
│       └── output.yaml
└── nginx-simple-patch
    ├── README.md
    ├── add-label.patch.yaml
    ├── fix-version.patch.yaml
    ├── kustomization.yaml
    ├── nginx-deployment.yaml
    ├── nginx-namespace.yaml
    ├── nginx-pdb.yaml
    ├── nginx-service.
```