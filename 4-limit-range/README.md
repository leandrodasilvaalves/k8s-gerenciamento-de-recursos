# Limit Range

O **Limit Range** protege o cluster kubernetes caso o desenvolvedor se esqueça de definir o `request` e o `limit` para o pod. O Limit Range afeta o processo de criação do pod, portanto suas regras só valerão para pods criados após sua definição aplicada no cluster. 

Exemplo de manifesto com `limit range`:
``` yaml
apiVersion: v1
kind: LimitRange
metadata: 
    name: limite-container
spec:
    limits:
        - max: 
            cpu: "800m"
            memory: "900Mi"
          min: 
            cpu: "150m"
            memory: "99Mi"
          default: 
            cpu: "250m"
            memory: "128Mi"
          defaultRequest: 
            cpu: "150m"
            memory: "100Mi"
          type: Container
``` 
> Caso nenhum valor seja informado para `limit` e `request` no deployment, este usará os valores `default` e `defaultRequest` do limit range

Após aplicar o manifesto use o comando abaixo para verificar os recursos do pod.
```
kubectl get pods <pod-name>
``` 

> Caso valores inválidos sejam definidos no manifesto de deployment o processo de criação do pod diparará um erro informando que a regra está sendo violada.

