# Upload Self-managed SSL to GKE Ingress GCE

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
