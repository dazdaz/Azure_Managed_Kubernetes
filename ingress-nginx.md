
in Nginx Ingress Controller version 0.22 Annotations nginx.ingress.kubernetes.io/add-base-url and nginx.ingress.kubernetes.io/base-url-scheme were removed.
https://github.com/kubernetes/ingress-nginx/releases

Refer to https://kubernetes.github.io/ingress-nginx/examples/rewrite/#rewrite-target on how to change it.

https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/nginx-configuration/annotations.md

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/enable-rewrite-log: "true"
    nginx.ingress.kubernetes.io/proxy-body-size: "0"
    nginx.ingress.kubernetes.io/rewrite-target: /$1
  name: rewrite-ingress
  namespace: default
spec:
  rules:
  - host: rewrite.bar.com
    http:
      paths:
      - backend:
          serviceName: http-svc
          servicePort: 80
        path: /(something/.*)
tls:
  -
    hosts:
      - rewrite.bar.com
    secretName: aks-dev-ingress-tls
```