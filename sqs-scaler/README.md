AWS IAM Policy:

```sh
aws iam create-policy --policy-name keda-sqs \
  --policy-document file://policy.json
```

Service account (IRSA) for Keda:

```sh
eksctl create iamserviceaccount --name keda-operator \
  --namespace keda \
  --cluster pegasus \
  --attach-policy-arn arn:aws:iam::310240692520:policy/keda-sqs \
  --region us-east-2 \
  --profile default \
  --approve
```

Test (sqs send-message):

```sh
for i in `seq 30`; do
  aws sqs send-message --queue-url 'https://sqs.us-east-2.amazonaws.com/310240692520/keda-queue' \
    --message-body "XXXX" \
    --region us-east-2 \
    --no-cli-pager \
    --output text
done
```