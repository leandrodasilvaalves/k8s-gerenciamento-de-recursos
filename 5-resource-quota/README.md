# Resource Quota

O `Resource Quota` limita os recursos a nível de namespaces.
Essa estratégia é interessante para cenários onde ambientes como `desenvolvimento` e `staging` estão alocados no mesmo cluster e são separados por namespaces. O Resource Quota evita que um namespace consuma mais recursos do que o outro.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata: 
    name: compute-resource
spec:
    hard:
        requests.cpu: "2"
        requests.memory: "4Gi"
        limits.cpu: "3"
        limits.memory: "6Gi"

```
## Exemplo:
Se criarmos 15 replicas de um determinado pod com request de cpu igual 200m sobre as regras do manifesto acima, apenas 10 replicas serão criadas porque 10x200=2000 que corresponde a dois núcleos de cpu. Logo as últimas 5 ferem as regras do **ResourceQuota** e não serão criadas.

Também é possível limitar a quantidade de replicas em um replicaset conforme mostrado no manifesto abaixo:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata: 
    name: compute-resource
spec:
    hard:
        pods: 12

```
> Caso tente criar um número maior do que o especificado no resource quota um erro será disparado e a quantidade de replicas não passarão do limite especificado.