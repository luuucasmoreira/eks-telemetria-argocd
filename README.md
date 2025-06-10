# Projeto conversão de temperatura

### Sobre o projeto
O projeto conversão de temperatura é um projeto desenvolvido em NodeJS. O projeto tem como objetivo ser um exemplo para a criação de ambiente com containers usando NodeJS.

### Observações do projeto
A aplicação é exposta usando a porta 8080

# Guia de Comandos - Conversão de Temperatura com K8s

## Requisitos

- **Docker**
- **kubectl**
- **k3d** ou **kind**

---

## Criar Cluster com K3d

```sh
k3d cluster create meucluster --servers 3 --agents 3 -p "30000:30000@loadbalancer"
```

---

## Criar Imagem e Publicar no Docker Hub

1. **Construa a imagem Docker:**
   
   Substitua pelo seu usuário e nome de repositório do Docker Hub, se desejar.
   
   ```sh
   docker build -t <seu-usuario-dockerhub>/conversao-temperatura:v1 .
   ```

2. **Faça login no Docker Hub (se necessário):**
   
   ```sh
   docker login
   ```

3. **Envie a imagem para o Docker Hub:**
   
   ```sh
   docker push <seu-usuario-dockerhub>/conversao-temperatura:v1
   ```

> **Observação:** Troque `<seu-usuario-dockerhub>` pelo seu usuário do Docker Hub e utilize o nome/tag que preferir para a imagem.

---

## Comandos do Kubernetes Utilizados

### Aplicar arquivos YAML

Acesse a pasta desejada ou informe o caminho completo dos arquivos YAML:

```sh
kubectl apply -f deployment.yaml
```

Após subir os deployments, acesse:
[http://localhost:30000](http://localhost:30000)

---

### Verificações

- **Verificar pods:**
  ```sh
  kubectl get pods
  ```
  > (Pode mudar para `deployments`, `replicasets`, `services`...)

- **Verificação geral:**
  ```sh
  kubectl get all
  ```

---

## Passo a Passo Rápido

Se estiver com tudo instalado, após clonar o repositório, rode:

```sh
kubectl apply -f k8s/deployment -f k8s/service.yaml
```

E verifique seu serviço em:
[http://localhost:30000](http://localhost:30000)