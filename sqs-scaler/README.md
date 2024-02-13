## AWS IAM Policy:

```sh
aws iam create-policy --policy-name keda-sqs-policy \
  --policy-document file://policy-sqs.json
```

## Service account (IRSA) for Keda:

```sh
eksctl create iamserviceaccount --name keda-operator \
  --namespace keda \
  --cluster CLUSTER \
  --attach-policy-arn arn:aws:iam::ACCOUNTID:policy/keda-sqs-policy \
  --region REGION \
  --profile default \
  --approve
```

## Test (sqs send-message):

```sh
for i in `seq 30`; do
  aws sqs send-message --queue-url 'https://sqs.REGION.amazonaws.com/ACCOUNTID/keda-queue' \
    --message-body "testmessage" \
    --region REGION \
    --no-cli-pager \
    --output text
done
```