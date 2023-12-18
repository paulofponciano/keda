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
  --override-existing-serviceaccounts \
  --approve
```

Output IRSA:

```sh
2023-12-18 07:59:37 [ℹ]  1 iamserviceaccount (keda/keda-operator) was included (based on the include/exclude rules)
2023-12-18 07:59:37 [!]  metadata of serviceaccounts that exist in Kubernetes will be updated, as --override-existing-serviceaccounts was set
2023-12-18 07:59:37 [ℹ]  1 task: { 
    2 sequential sub-tasks: { 
        create IAM role for serviceaccount "keda/keda-operator",
        create serviceaccount "keda/keda-operator",
    } }2023-12-18 07:59:37 [ℹ]  building iamserviceaccount stack "eksctl-pegasus-addon-iamserviceaccount-keda-keda-operator"
2023-12-18 07:59:38 [ℹ]  deploying stack "eksctl-pegasus-addon-iamserviceaccount-keda-keda-operator"
2023-12-18 07:59:38 [ℹ]  waiting for CloudFormation stack "eksctl-pegasus-addon-iamserviceaccount-keda-keda-operator"
2023-12-18 08:00:09 [ℹ]  waiting for CloudFormation stack "eksctl-pegasus-addon-iamserviceaccount-keda-keda-operator"
2023-12-18 08:00:10 [ℹ]  serviceaccount "keda/keda-operator" already exists
2023-12-18 08:00:10 [ℹ]  updated serviceaccount "keda/keda-operator"
```