# herpai-helm-chart
This repo contains Helm charts for [HerpAI app](https://github.com/openbiocure/HerpAI).

## Instructions

### 1. Create your secrets in your kubernetes cluster:

```bash
kubectl create secret generic herpai-secrets \
  --from-literal=SONNET_API_KEY={your-sonnet-api-key} \
  --from-literal=OPENAI_API_KEY={your-openai-api-key}
```

### 2. Add the HerpAI chart to Helm

```bash
helm repo add herpai-chart https://ngonsoto.github.io/herpai-helm-chart/
helm repo update
```

### 3. Install the HerpAI chart to your cluster

```bash
helm install herpai herpai-chart/herpai-chart
```

### 4. Get the app IP and port
```bash
export SERVICE_IP=$(kubectl get svc --namespace default herpai-herpai-chart --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
echo http://$SERVICE_IP:8080
```
