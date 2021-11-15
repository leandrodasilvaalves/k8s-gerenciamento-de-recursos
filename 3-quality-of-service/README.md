# QoS - Quality of Services
 
Um ponto importante em relação ao uso do request e do Limit é a configuração do QoS para garantir a qualidade do serviço do meu pod.
- **BestEffort**: sem request e limits definidos
- **Burstable**: requests e limits com valores diferentes
- **Guaranteed**: request e limits com valores iguais

Esses níveis significam o quanto o kubernetes vai se preocupar manter os pods ativos. Quando houver qualquer problema no cluster e o kubernetes precisar eliminar alguns pods, isso acontecerá de acordo com a qualidade do serviço definida sendo que os pods com `BestEffort` serão os primeiros a serem removidos, os do tipo `Burstable` em segundo lugar e por fim os pods com `Guaranteed`.

## Exemplos:
### BestEffort
```yaml
...
spec:
    containers:
    - name: resource-container
    image: gcr.io/k8s-staging-e2e-test-images/resource-consumer:1.9 
    resources: {}
...
```
### Burstable
```yaml
...
spec:
    containers:
    - name: resource-container
    image: gcr.io/k8s-staging-e2e-test-images/resource-consumer:1.9 
    resources:
        requests:
            memory: "32Mi"
            cpu: "100m"
        limits:
            memory: "64Mi"
            cpu: "500m"
...
```
### Guaranteed
```yaml
...
spec:
    containers:
    - name: resource-container
    image: gcr.io/k8s-staging-e2e-test-images/resource-consumer:1.9 
    resources:
        requests:
        memory: "32Mi"
        cpu: "100m"
        limits:
        memory: "32Mi"
        cpu: "100m"
...
```