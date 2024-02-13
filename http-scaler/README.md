## HTTP add-on:

```sh
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda \
  --set serviceAccount.name=keda-operator \
  --create-namespace
helm install http-add-on kedacore/keda-add-ons-http --namespace keda
```

docs/ref/v0.2.0:

https://github.com/kedacore/http-add-on/blob/main/docs/ref/v0.2.0/http_scaled_object.md