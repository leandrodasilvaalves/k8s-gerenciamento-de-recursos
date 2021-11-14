# Resource Request e Resource Limits

O resource request e resource limit visam proteger tanto a aplicação quanto o cluster kubernetes.
- ao configurar o resource request eu estou garantindo que a aplicação terá os recusrsos mínimos para sua execução.
- ao configurar o resource limit eu estou protegendo o meu cluster contra bugs na aplicação que podem gerar consumo excessivo de cpu e memória.

```
 kubectl top pod <pod-name>
```
Caso o comando acima não estiver instalado, executar o comando abaixo para instalar:

```
 kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Repositório do [Kubernetes Metrics Server](https://github.com/kubernetes-sigs/metrics-server)

O google disponibilizou a imagem [gcr.io/k8s-staging-e2e-test-images/resource-consumer:1.9](https://console.cloud.google.com/gcr/images/kubernetes-e2e-test-images/GLOBAL/resource-consumer@sha256:284fcd047cdec35e1b212919bd878ba5ef72f1da12f49ddc199d219fa8b64f4a/details?tag=1.5) para fins de estudos de consumo de cpu e memória. Os comandos abaixo fazem com o container consuma os recursos de acordo com o valor informado durante o tempo desejado. Segue o [link da página oficial](https://pkg.go.dev/k8s.io/kubernetes/test/images/resource-consumer)

```
 curl --data "megabytes=80&durationSec=30" http://167.172.13.212/ConsumeMem
 curl --data "millicores=130&durationSec=60" http://167.172.13.212/ConsumeCPU
```