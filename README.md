export NAME=matomo

# new chart 
helm init ${NAME}

# template out the chart
helm template ${NAME} . 

# Apply the template into your namespace
helm template matomo . | kubectl apply -f - 


# common tasks
```
# pop a shell into the container
kubectl get pods # make node of the pod id
kubectl exec -it $pod_id /bin/bash

# view logs of the container
stern matomo # recommended
kubectl logs $pod_id
# both of these commands have a -f (follow) option

```

# discovery
```
kubectl describe pod $pod_id # see the running description of the pod
kubectl get svc # get the service objects that were created
kubectl get svc -o wide  # wide output is fun
kubectl get ingress # see what's exposed as an ingress (external to the cluster)
kubectl get statefulset (mariadb is a statefulset)
kubectl get deployments
kubectl delete po $pod_id (delete a pod)
kubectl get pvc #show pvcs and if they are bound
kubectl port-forward $pod_id $source_port:dest_port # expose a pods contianer port as localhost
example:
kubectl port-forward matomo-mariadb-0 3306:3306  # forward 3306 on mariadb
```

# start from scratch
```
helm template matomo . | kubectl delete -f -
kubectl get pvc
kubectl get pods
kubectl get statefulset
kubectl delete pvc data-matomo-mariadb-0
```

kubectl port-forward {{ pod }} 3306:3306



# TODO 
[] put plugins and data into a pvc (mounted at /data)
[] inject bootstrap.php from a configmap into /var/www/html
[] perhaps pull in location data
[] simplify entrypoint script, add error logging



# References
inspiration from the official matomo docker, and crazy-max
https://github.com/crazy-max/docker-matomo/tree/master/examples/kubernetes
