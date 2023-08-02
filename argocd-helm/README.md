# argocd helm with kustomize

helm chart 를 kustomize 이용해서 설치

## manifests(yaml) 생성

`$ kubectl kustomize --enable-helm . >> output.yaml` 

## install

`$ kubectl kustomize --enable-helm . | kubectl apply -f -` 
