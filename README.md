KEDA | Kubernetes Event-driven Autoscaling

https://keda.sh/

Keda deploy with Helm:

```sh
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda \
  --set serviceAccount.create=false \
  --set serviceAccount.name=keda-operator
```