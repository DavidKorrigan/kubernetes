# kubernetes

## Cluster configuration
path: ~/.kube/config
```sh
# Display configuration
kubectl config view
```

## Basic commands
### Retrieve information
```sh
# Display context
kubectl config get-contexts
# Display the services
kubectl get services
# Display the nodes
kubectl get nodes
# Display the pods
kubectl get pods
# -o wide allows to add details
kubectl get nodes -o wide
kubectl get services -o wide
kubectl get pods -o wide
# Get description of a specific item
kubectl describe services {{service_name}}
kubectl describe services s1
kubectl describe nodes {{node_name}}
kubectl describe nodes host41
kubectl describe pods {{pod_name}}
kubectl describe pods web1
# --show-labels
kubectl get services --show-labels
kubectl get nodes --show-labels
kubectl get pods --show-labels
# Display nodes & pods
kubectl get all
# Display namespace
kubectl get namespace
# Display Persistent Volume
kubectl get pv
# Display Persistent Volume Claim
kubectl get pvc
```

### Apply configuration
```sh
# Apply specific file
kubectl apply -f {{file_name}}
kubectl apply -f s1.yml
# Apply all the file from the folder
kubectl apply -f .
```

### Debug
```sh
# Get a shell from a pod
kubectl exec -it {{pod_name}} -- sh
kubectl exec -it debug -- sh
# Install a bin on a pod
apk add curl
# port forwarding on pod
kubectl port-forward {{pod_name}} 8000:80
kubectl port-forward debug 8000:80
curl {{pod_name}}:8000
curl {{node_name}}:30000
```

### Delete item
```sh
# Delete pod
kubectl delete pods {{pod_name}}
kubectl delete pods debug
# Force to delete everything
kubectl delete all --all --force
```

### Set asset to namepace
```sh
kubectl apply -f {{file_name}} --namespace={{name_namespace}}
kubectl apply -f web-pod.yml --namespace=production
```

### Context
```sh
# Create & set context
kubectl config set-context {{name_context}} --cluster={{name_cluster}} --user={{name_user}} --namespace={{name_ns}}
kubectl config set-context dev --cluster=cluster.local --user=kubernetes-admin --namespace=development
# Use context
kubectl config use-context {{name_context}}
kubectl config use-context dev
```

```sh
# Copy from pod
kubectl cp web:/etc/nginx/nginx.conf /tmp/nginx.conf

kubectl create configmap nginx-conf --from-file=nginx.conf
```

kubectl explain ..