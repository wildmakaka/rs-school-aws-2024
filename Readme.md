# [Task 5: Simple Application Deployment with Helm](https://github.com/rolling-scopes-school/tasks/blob/master/devops/modules/3_ci-configuration/task_5.md)

<br/>

Date:  
2024.11.10

<br/>

```
$ git clone https://github.com/wildmakaka/helm-charts.git
$ cd helm-charts/wordpress-0.1.1/
$ helm install wordpress .
```

<br/>

```
$ helm list
NAME     	NAMESPACE	REVISION	UPDATED                                	STATUS  	CHART              	APP VERSION
wordpress	default  	1       	2024-11-10 11:43:22.854796059 +0000 UTC	deployed	wordpress-app-0.1.1	0.1.1   
```

<br/>

```
$ helm status wordpress
NAME: wordpress
LAST DEPLOYED: Sun Nov 10 11:43:22 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```



<br/>

```
$ kubectl get pods
NAME                                                 READY   STATUS    RESTARTS   AGE
minikube-wordpress-app-deployment-85d6f48557-z7v4w   1/1     Running   0          2m42s
         37s
```


<br/>

### Add NGROK ingress

```
$ export NGROK_DOMAIN="hugely-amusing-owl.ngrok-free.app"
```

<br/>

```yaml
$ envsubst << 'EOF' | cat | kubectl create -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ngrok-wordpress-ingress-service
spec:
  ingressClassName: ngrok
  rules:
    - host: ${NGROK_DOMAIN}
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: minikube-wordpress-app-cluster-ip-service
                port:
                  number: 8080
EOF
```


<br/>

browser ->  
http://hugely-amusing-owl.ngrok-free.app/wp-admin/setup-config.php


<br/>

![Application](../img/task5/task5_pic_01_accessible_from_web.png)

<br/>

```
$ helm uninstall wordpress
```

<br/><br/>

---

<br/>

**Marley**

Any questions in english: <a href="https://gitops.ru/chat/">Telegram Chat</a>  
Любые вопросы на русском: <a href="https://gitops.ru/chat/">Телеграм чат</a>
