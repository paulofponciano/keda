# KEDA | Kubernetes Event-driven Autoscaling

https://keda.sh/

## Keda deploy with Helm:

> [!NOTE]
> Caso não faça a criação da service account utilizando EKSCTL (IRSA), altere o parâmetro '--set serviceAccount.create=false' para '--set serviceAccount.create=true'. A criação do IRSA é descrita em [sqs-scaler](sqs-scaler/README.md#Service-account-(IRSA)-for-Keda).

```sh
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda \
  --set serviceAccount.create=false \
  --set serviceAccount.name=keda-operator
```