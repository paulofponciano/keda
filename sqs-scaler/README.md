## Create SQS queue:

```sh
aws sqs create-queue --queue-name keda-sqs --region REGION
```

## AWS IAM Policy:

```sh
aws iam create-policy --policy-name keda-sqs-policy \
  --policy-document file://policy-sqs.json
```

## Service account (IRSA) for Keda:

```sh
eksctl create iamserviceaccount --name keda-operator \
  --namespace keda \
  --cluster pegasus \
  --attach-policy-arn arn:aws:iam::ACCOUNTID:policy/keda-sqs-policy \
  --region REGION \
  --profile default \
  --approve
```

## Test (sqs send-message):

```sh
for i in `seq 35`; do
  aws sqs send-message --queue-url 'https://sqs.us-east-2.amazonaws.com/310240692520/keda-queue' \
    --message-body "testmessage" \
    --region us-east-2 \
    --no-cli-pager \
    --output text
done
```