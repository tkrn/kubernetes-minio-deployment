
# kubernetes-minio-deployment
* * *
In summary, this is my implementation of MinIO on in a Kubernetes cluster. This is deployment is done entirely in it's own namespace. It was my desire to keep the data plane from the application as isolated as possible. 

## Description of files:
| File  | Description |
| :------------- |:-------------|
|  minio-namespace.yml | [Namspace spec](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) |
| minio-storageclass.yml | [Storage Class spec](https://kubernetes.io/docs/concepts/storage/storage-classes/) |
| minio-pv.yml | [Persistent Volume spec](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) |
| minio-pvc.yml | [Persistent Volume Claim Rule spec](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#expanding-persistent-volumes-claims) |
| minio-secrets.yml | [Secrets spec](https://kubernetes.io/docs/concepts/configuration/secret/) for MINIO_ROOT_USER & MINIO_ROOT_PASSWORD |
| minio-tls-secrets.yml | [Secrets spec](https://kubernetes.io/docs/concepts/configuration/secret/) fo public.crt & private.key MinIO SSL certificate use |
| minio-deployment.yml | [Deployment spec](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) |
| minio-svc.yml | [Service spec](https://kubernetes.io/docs/concepts/services-networking/service/) |

A quick note about secrets, they are encoded in base64 meaning the data will need to be decoded to see their values. 

The default username & password within the the minio-secrets.yml file is **minio/minio**.

## How to deploy
Here's a quick starter, order matter:

```
kubectl create -f minio-namespace.yml
kubectl create -f minio-storageclass.yml
kubectl create -f minio-pv.yml
kubectl create -f minio-pvc.yml
kubectl create -f minio-secrets.yml
kubectl create -f minio-tls-secrets.yml
kubectl create -f minio-deployment.yml
kubectl create -f minio-svc.yml
```

For microk8s, it would be like:
```
microk8s kubectl create -f minio-namespace.yml
microk8s kubectl create -f minio-storageclass.yml
microk8s kubectl create -f minio-pv.yml
microk8s kubectl create -f minio-pvc.yml
microk8s kubectl create -f minio-secrets.yml
microk8s kubectl create -f minio-tls-secrets.yml
microk8s kubectl create -f minio-deployment.yml
microk8s kubectl create -f minio-svc.yml
```

This is licensed under the [MIT license](LICENSE).
