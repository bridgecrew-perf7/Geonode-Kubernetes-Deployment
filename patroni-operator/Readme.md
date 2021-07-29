# Run postgres-operator spilo
check further documentation under: https://opensource.zalando.com/postgres-operator/docs/quickstart.html#deployment-options

start apply operator with api and ui with kustomize
```bash
kubectl -n spilo apply .
```

check if everything is started correctly
```bash
kubectl get all -n spilo
```

this must show:
```bash
NAME                                        READY   STATUS    RESTARTS   AGE
pod/postgres-operator-689dc5bcf4-pcb75      1/1     Running   0          5m
pod/postgres-operator-ui-77f8cb6d84-5c8ds   1/1     Running   0          5m

NAME                           TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
service/postgres-operator      ClusterIP      10.105.232.146   <none>         8080/TCP       5m
service/postgres-operator-ui   LoadBalancer   10.96.55.204     10.96.55.204   80:31575/TCP   5m

NAME                                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/postgres-operator      1/1     1            1           5m
deployment.apps/postgres-operator-ui   1/1     1            1           5m

NAME                                              DESIRED   CURRENT   READY   AGE
replicaset.apps/postgres-operator-689dc5bcf4      1         1         1       5m
replicaset.apps/postgres-operator-ui-77f8cb6d84   1         1         1       5m
```
having an external IP addr vor the operator-ui service, one pod for the operator one for the ui.

Now databases can be created using manifest described under: https://opensource.zalando.com/postgres-operator/docs/user.html#connect-to-postgresql



