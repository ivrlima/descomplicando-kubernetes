## descomplicando-kubernetes

 - Instalar kind na maquina local 
 - Instalar binario kubectl para execução dos comandos 

 
## Tecnologia utilizadas:
 
 - kind 
 - kubectl 
 - Ubuntu 24.04
 - yaml 
 - auto complet  


 
 ## Clonar o repositorio 
 ```git 
 git clone https://github.com/ivrlima/descomplicando-kubernetes.git 
 ``` 
  
 ## Criar o cluster baseado no arquivo de configuração 

  ```vim 
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker

  ```

 ```kind
 
 cd day-1 && 
 kind create cluster --config kind-cluster.yaml --name k8s-kind
  
 ``` 
 ## Executando dry-run para capturar o yaml referente ao pod 
 ```kubect
  kubectl run --image nginx --port 80 giropops-giraia --dry-run=client -o yaml
 ```
```yaml  
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: giropops-giraia
  name: giropops-giraia
spec:
  containers:
  - image: nginx
    name: giropops-giraia
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

## Criando o manifesto K8s apartir do comando dry-run=client 

```kubectl
 kubectl run --image nginx --port 80 giropops-giraia --dry-run=client -o yaml > pod.yaml 

```
## Aplicando a configuração apos a criação do pod.yaml 

```kubectl
 kubectl apply -f pod.yaml 

```

## Acompanhando a criação do pod com o -w 

```kubectl
 
 kubectl get pods -w  

```

### Obs: o auto complete não funciona quando adicionamos o alias k="kubectl"
### No .bashrc somente utilizando kubectl run <tab>


## [Referencia][https://kind.sigs.k8s.io/docs/user/quick-start/]
