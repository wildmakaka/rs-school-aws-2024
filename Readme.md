# How to connect to cloud


<br/>

```
$ cd ~/tmp

$ curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-linux-x86_64.tar.gz

$ tar -zxvf google-cloud-cli-linux-x86_64.tar.gz

$ cd google-cloud-sdk/

$ ./install.sh

$ source ~/.bashrc
```

<br/>

```
// connect
$ gcloud auth login
$ gcloud cloud-shell ssh
```


# How to run in linux

<br/>

```
// kubectl setup
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/
```

<br/>

```
// minikube setup
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```


<br/>

```
// specify minikube params
$ export \
    PROFILE=${USER}-minikube \
    CPUS=4 \
    MEMORY=8G \
    HDD=20G \
    DRIVER=docker \
    KUBERNETES_VERSION=${LATEST_KUBERNETES_VERSION}
```

<br/>

```
// minikube run
$ {
    minikube --profile ${PROFILE} config set memory ${MEMORY}
    minikube --profile ${PROFILE} config set cpus ${CPUS}
    minikube --profile ${PROFILE} config set disk-size ${HDD}

    minikube --profile ${PROFILE} config set driver ${DRIVER}

    minikube --profile ${PROFILE} config set kubernetes-version ${KUBERNETES_VERSION}
    minikube start --profile ${PROFILE} --embed-certs

    // Enable ingress
    minikube addons --profile ${PROFILE} enable ingress

    // Enable registry
    // minikube addons --profile ${PROFILE} enable registry
}
```

<br/>

```
// minikube check
$ kubectl get nodes
```

<br/>

```
// run simple application
$ kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml
```
<br/>

```
// check the running application
$ kubectl get pods
```

<br/>

![Application](/img/kubectl-shell.png)


That is all


<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://gitops.ru/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://gitops.ru/chat/">Телеграм чат</a>
