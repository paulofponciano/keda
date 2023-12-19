HTTP add-on:

```sh
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda \
  --set serviceAccount.name=keda-operator \
  --create-namespace
helm install http-add-on kedacore/keda-add-ons-http --namespace keda
```