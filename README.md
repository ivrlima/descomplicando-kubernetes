## descomplicando-kubernetes

 - Instalar kind na maquina local 
 - Instalar binario kubectl para execução dos comandos 


## Instalando o Auto Complete 
```
source <(kubectl completion bash) # configura o autocomplete na sua sessão atual (antes, certifique-se de ter instalado o pacote bash-completion).

echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete permanentemente ao seu shell.

echo k="kubectl" >> ~/.bashrc 

source ~/.bashrc

--obs: para funcionar o auto-complete com alias, execute o comando abaixo.. 

complete -F __start_kubectl k 
 
```
## Instalancdo kubectl....
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version --client
``` 
## Tecnologias utilizadas:
  
 - kind 
 - kubectl 
 - Ubuntu 24.04
 - yaml 
 - auto complete  


 
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
-- Kind: Uma ferramenta para execução de contêineres Docker que simulam o funcionamento de um cluster Kubernetes. É utilizado para fins didáticos, de desenvolvimento e testes. O Kind não deve ser utilizado para produção;

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


## [Referencia][https://kind.sigs.k8s.io/docs/user/quick-start/]
