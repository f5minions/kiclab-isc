# k8s Ingress Controller with AppProtect Lab for ISC

**NOTE: A working k8s environment has been setup **

```
helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
helm install my-ingress nginx-stable/nginx-ingress --set controller.image.repository=richardincyberspace/nap --set controller.nginxplus=true --set controller.image.tag=1.8.0 --set controller.appprotect.enable=true
```

> Setup `cafe-app` demo app

```
kubectl apply -f https://raw.githubusercontent.com/richardincyberspace/kiclab-isc/master/demo-cafe-app.yaml
```