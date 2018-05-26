# Helm - Gestor de paquetes

## Instalar Helm

- Descargar:

https://github.com/kubernetes/helm/releases

- Descomprimir

`$ tar -zxvf helm-$VERSION-linux-amd64.tgz`

- Colocar el binario en su sitio

`$ sudo mv linux-amd64/helm /usr/local/bin`

## Iniciar 

`$ helm init`

- Comprobar

`$ kubectl --namespace=kube-system get pods --selector app=helm`

```
NAME                            READY     STATUS    RESTARTS   AGE
tiller-deploy-78f96d6f9-8kc88   1/1       Running   0          2m
```

## Autorización

Ejecutar estas líneas para otorgar autorización a Helm

`$ kubectl -n kube-system patch deployment tiller-deploy -p '{"spec": {"template": {"spec": {"automountServiceAccountToken": true}}}}'`

`$ kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default`

## Vamos a desplegar Dokuwiki por ejemplo

`$ helm install --name my-doku --set persistence.apache.storageClass=standard,persistence.dokuwiki.storageClass=standard stable/dokuwiki`