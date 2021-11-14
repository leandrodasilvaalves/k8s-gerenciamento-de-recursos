# Horizontal Pod Autoscaler - HPA

Este é um recurso que permite escalibilidade automática no kubernetes quando parametrizado em conjunto com `requests` e `limit`.

Exemplo de manifesto HPA:

```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-deploy
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    app: resource-container
  minReplicas: 1
  maxReplicas: 20
  targetCPUUtilizationPercentage: 50
```
Use o comando abaixo para aplicar o manifesto no cluster:
```bash
Kubectl apply - hpa-file.yaml
```
Utilizar o comando abaixo para aumentar o consumo de cpu dos pods:

``` 
 curl --data "millicores=130&durationSec=60" http://<external-ip>/ConsumeCPU
```

Por fim utilizar os comandos abaixo para ver o auto escalonamento de formas diferentes:
```
kubectl get hpa
kubectl top pods
kubectl get pods
```

