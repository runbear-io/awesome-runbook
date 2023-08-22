# Decoding Secrets

This runbook is to decode Kubernetes secrets.

## Procedure

### 1. Identify the Secret

First, find the secret you need to decode. List all available secrets in the namespace using the command below. Identify the one you need, and make a note of its name.

```sh
kubectl get secrets
```

### 2. Extract the Secret

Extract the secret's encoded value using the command below. Replace `{{SECRET_NAME}}` with the actual secret name and `{{KEY}}` with the specific key you need.

```sh
kubectl get secret {{SECRET_NAME}} -o jsonpath='{.data.{{KEY}}}'
```

### 3. Decode the Secret

The secret's value is base64 encoded. To decode it, use the following command:

```sh
echo '{{ENCODED_SECRET}}' | base64 --decode
```

Replace `{{ENCODED_SECRET}}` with the encoded value from step 2.

### 4. Cleanup (Optional)

Ensure you clear the terminal history or any other temporary locations where the secret may have been exposed. It's crucial to maintain the security of sensitive information.

## Expectation

The secret value is intended to be printed out.
