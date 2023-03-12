# 개요
이미 기존에 쿠버네티스 리소스가 있는 상황에서 helm으로 릴리즈 하면 어떻게 되는지 테스트

# 테스트 방법
* 쿠버네티스 리소스 배포
```shell
kubectl apply -f deploy.yaml
```

> 아래 helm 차트 release는 에러가 발생

* helm 차트 release
```shell
helm install helm-test ./charts
```

# 해결방법
* 수동으로 기존 쿠버네티스 리소스에 helm 식별자 추가
```shell
NAME=helm-test-nginx
RELEASE=helm-test
NAMESPACE=default

kubectl annotate deployment $NAME meta.helm.sh/release-name=$RELEASE
kubectl annotate deployment $NAME meta.helm.sh/release-namespace=$NAMESPACE
kubectl label deployment $NAME app.kubernetes.io/managed-by=Helm
```

# 참고자료
* https://helm.sh/docs/chart_best_practices/labels/
