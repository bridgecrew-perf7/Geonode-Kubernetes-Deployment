# Geonode Kustomize Deployment Script

this kubernetes kustomize application is written to run geonode in kubernetes. This is a work in progress project, with a number of known issues. I'm planning to address the issues listed below. Afterwards I will move this application from kustomize to helmchart to implement a wider range on functionality and flexibility of the installation.


# Installation instructions

The current kustomize implementation is based on local volumes provided by minikube. To run this installation in another kubernetes you have to change the specified storageClassName in PersistantVolume creation.

## installing minikube 

See https://minikube.sigs.k8s.io/docs/start/ for howTo install minikube ... 


## install geonode

having your minikube cluster configured correctly you can start the installation via:
```bash
kubectl apply -k base/
```
Now all services,deployments and so are setup on your minikube cluster. Afterwards you must make the service available from outside the cluster. Therefore, run (https://minikube.sigs.k8s.io/docs/handbook/accessing/):
```bash
minikube tunnel
```

This allows you to access exposed kubernetes services from your host machine. You can get the IP-address of the exposed service via:
```bash
kubectl get service -l run=nginx
```
This should look something like:
```bash
NAME      TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
geonode   LoadBalancer   10.103.109.246   10.103.109.246   80:31444/TCP,443:32431/TCP   18m
```

You can access the geonode installtion via the "EXTERNAL-IP" address shown. If you get an error "503 unknown gateway" you have to wait some more time until the django containers is fully started.

## known issues/todos

- unable to upload layers, something still broken in geoserver
- 503 after register new user

- move postgis,geoserver to a stateful set
- move pv creation out of base
- introduce celary
- reduce amount of volumes