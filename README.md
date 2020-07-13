# Upload Self-managed SSL to GKE Ingress GCE

#### upload your ssl sertificate, for example im use wildcard ssl

```
ls 
star_yourdomain.crt  star_yourdomain.csr  star_yourdomain.key
```
```
gcloud compute ssl-certificates create ssl-sectigo-yourdomain --certificate star_yourdomain.crt --private-key star_yourdomain.key

Created [https://www.googleapis.com/compute/v1/projects/zeus-cloud/global/sslCertificates/ssl-sectigo-yourdomain].
NAME                    TYPE          CREATION_TIMESTAMP             EXPIRE_TIME                    MANAGED_STATUS
ssl-sectigo-yourdomain  SELF_MANAGED  2020-07-13T11:04:44.497-07:00  2021-09-26T16:59:59.000-07:00
```

#### edit your ingress for use Self-managed SSL we upload via gcloud cli
```
ingress.gcp.kubernetes.io/pre-shared-cert: "ssl-sectigo-yourdomain"
```
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: prod-ingress
  annotations:
    kubernetes.io/ingress.global-static-ip-name: "prod-ingress"
    ingress.gcp.kubernetes.io/pre-shared-cert: "ssl-sectigo-yourdomain"
spec:
  rules:
    - host: yourdomain.com
      http:
        paths:
        - backend:
            serviceName: prod-frontend-redirect-www
            servicePort: 80
    - host: www.yourdomain.com
      http:
        paths:
        - backend:
            serviceName: prod-frontend
            servicePort: 80
    - host: api.yourdomain.com
      http:
        paths:
        - backend:
            serviceName: prod-api
            servicePort: 80
```
#### apply change in ingress yaml
```
kubectl apply -f production-ingress.yaml
```
