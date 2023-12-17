AWS IAM Policy:

```sh
aws iam create-policy --policy-name keda-sqs \
  --policy-document file://policy.json
```

Service account (IRSA) for Keda:

```sh
eksctl create iamserviceaccount --name keda-operator \
  --namespace keda \
  --cluster poc-eks \
  --attach-policy-arn arn:aws:iam::310240692520:policy/keda-sqs \
  --region us-east-1 \
  --profile default \
  --approve
```