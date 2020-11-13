# k8s Ingress Controller with AppProtect Lab for ISC

**NOTE: A working k8s environment has been setup for you in the Blueprint **

```
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
helm install my-ingress nginx-stable/nginx-ingress --set controller.image.repository=richardincyberspace/nap \
  --set controller.nginxplus=true --set controller.image.tag=1.8.0 --set controller.appprotect.enable=true \
  --version 0.6.1
```

> Setup `cafe-app` demo app

```
kubectl apply -f https://raw.githubusercontent.com/richardincyberspace/kiclab-isc/master/demo-cafe-app.yaml
kubectl get service
```

> Deploy Ingress Resource
```
curl https://raw.githubusercontent.com/richardincyberspace/kiclab-isc/master/cafe-ingress.yaml | sed "s/127.0.0.1/`kubectl get svc | grep syslog-svc | awk '{print $3}'`/g" | kubectl apply -f -
kubectl  describe ingress cafe-ingress
```
> Run the Demo
```
export IC=`kubectl get svc  | grep ingress | awk '{print $3}'`
```

```
curl --resolve cafe.example.com:443:$IC https://cafe.example.com:443/coffee -k
```

```
curl --resolve cafe.example.com:443:$IC "https://cafe.example.com:443/coffee/<script>" -k
```

```
kubectl exec -it `kubectl get pod | grep syslog| awk '{print $1}'` -- tail  /var/log/messages
```
