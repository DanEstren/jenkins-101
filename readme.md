# 🚀 **Instalação do Jenkins BlueOcean com Docker**

---

## 📺 **Vídeo do Curso Completo**
Assista o curso completo de 1 hora no YouTube:  
[https://www.youtube.com/watch?v=6YZvp2GwT0A](https://www.youtube.com/watch?v=6YZvp2GwT0A)

---

## 🐳 **Construa a Imagem Docker do Jenkins BlueOcean**

### Opção 1: Construir a imagem localmente
```bash
docker build -t myjenkins-blueocean:2.414.2 .
```

### Opção 2: Usar a imagem pré-construída (versão 2.332.3-1)
```bash
docker pull devopsjourney1/jenkins-blueocean:2.332.3-1
docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1
```

---

## 🌐 **Criar a Rede 'jenkins'**
```bash
docker network create jenkins
```

---

## 🖥️ **Executar o Contêiner Jenkins**

### Para **MacOS/Linux**:
```bash
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.2
```

### Para **Windows** (PowerShell):
```powershell
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2
```

---

## 🔑 **Obter a Senha Inicial**
```bash
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

---

## 🌍 **Acessar o Jenkins**
Abra no navegador:  
🔗 [http://localhost:8080](http://localhost:8080)

---

## 📚 **Referência de Instalação**
Documentação Oficial:  
[https://www.jenkins.io/doc/book/installing/docker/](https://www.jenkins.io/doc/book/installing/docker/)

---

## 🔄 **Configurar Comunicação com Docker Host**

### **alpine/socat** (para conectar Jenkins ao Docker Desktop)
```bash
docker run -d --restart=always -p 127.0.0.1:2376:2375 \
  --network jenkins -v /var/run/docker.sock:/var/run/docker.sock \
  alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
```

### Obter IP do Contêiner
```bash
docker inspect <container_id> | grep IPAddress
```

---

## 🐍 **Usar Agente Python Personalizado**
```bash
docker pull devopsjourney1/myjenkinsagents:python
```
**Dica:** Use este agente em seus *Pipelines* para execução de scripts Python! 🐍

---

✨ **Pronto! Seu ambiente Jenkins está configurado e pronto para automatizar!** ✨
