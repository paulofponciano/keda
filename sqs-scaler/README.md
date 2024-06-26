> [!NOTE]
> Não esqueça de substituir os valores de REGION, ACCOUNTID, CLUSTER na 'policy-sqs.json' e no 'scaledobject.yaml' e também nos comandos.

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
  --cluster CLUSTER \
  --attach-policy-arn arn:aws:iam::ACCOUNTID:policy/keda-sqs-policy \
  --region REGION \
  --profile default \
  --approve
```

## Test (sqs send-message):

```sh
for i in `seq 35`; do
  aws sqs send-message --queue-url 'https://sqs.REGION.amazonaws.com/ACCOUNTID/keda-queue' \
    --message-body "testmessage" \
    --region REGION \
    --no-cli-pager \
    --output text
done
```