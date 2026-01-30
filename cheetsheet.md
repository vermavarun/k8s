# Kubernetes Command Cheatsheet

Complete kubectl command reference aligned with Kubernetes mastery roadmap.

---

## 📋 Table of Contents
1. [Cluster Management](#cluster-management)
2. [Core Concepts](#core-concepts)
3. [Workload Resources](#workload-resources)
4. [Services & Networking](#services--networking)
5. [Storage](#storage)
6. [Configuration](#configuration)
7. [RBAC & Security](#rbac--security)
8. [Monitoring & Debugging](#monitoring--debugging)
9. [Advanced Operations](#advanced-operations)

---

## 🎯 Cluster Management

### Cluster Info & Configuration

| Command | Description |
|---------|-------------|
| `kubectl cluster-info` | Display cluster endpoint information |
| `kubectl version --short` | Show client and server version |
| `kubectl config view` | View kubeconfig file |
| `kubectl config current-context` | Display current context |
| `kubectl config get-contexts` | List all available contexts |
| `kubectl config use-context <context-name>` | Switch to different context |
| `kubectl config set-context <context> --namespace=<ns>` | Set default namespace for context |
| `kubectl config delete-context <context-name>` | Delete context from kubeconfig |
| `kubectl api-resources` | List all available API resources |
| `kubectl api-versions` | List all API versions |
| `kubectl explain <resource>` | Get documentation for resource |
| `kubectl explain <resource>.spec` | Get spec documentation |

### Namespaces

| Command | Description |
|---------|-------------|
| `kubectl get namespaces` | List all namespaces |
| `kubectl get ns` | List namespaces (short) |
| `kubectl create namespace <name>` | Create new namespace |
| `kubectl delete namespace <name>` | Delete namespace |
| `kubectl describe namespace <name>` | Show namespace details |
| `kubectl config set-context --current --namespace=<name>` | Set default namespace |
| `kubectl label namespace <name> env=prod` | Add label to namespace |
| `kubectl get all -n <namespace>` | Get all resources in namespace |

---

## 📦 Core Concepts

### Pods

| Command | Description |
|---------|-------------|
| `kubectl get pods` | List pods in current namespace |
| `kubectl get pods -A` | List pods in all namespaces |
| `kubectl get pods -n <namespace>` | List pods in specific namespace |
| `kubectl get pods -o wide` | List pods with additional details (node, IP) |
| `kubectl get pods --show-labels` | Show pod labels |
| `kubectl get pods -l <label-selector>` | Filter pods by label |
| `kubectl get pods --field-selector status.phase=Running` | Filter by field selector |
| `kubectl get pods --sort-by=.metadata.creationTimestamp` | Sort pods by creation time |
| `kubectl run <pod-name> --image=<image>` | Create pod from image |
| `kubectl run <pod-name> --image=<image> --dry-run=client -o yaml` | Generate pod YAML |
| `kubectl run <pod-name> --image=<image> --command -- <cmd> <arg1>` | Run pod with command |
| `kubectl describe pod <pod-name>` | Show detailed pod information |
| `kubectl delete pod <pod-name>` | Delete pod |
| `kubectl delete pod <pod-name> --grace-period=0 --force` | Force delete pod immediately |
| `kubectl delete pods --all` | Delete all pods in namespace |
| `kubectl get pod <pod-name> -o yaml` | Get pod definition in YAML |
| `kubectl get pod <pod-name> -o json` | Get pod definition in JSON |
| `kubectl edit pod <pod-name>` | Edit pod configuration |
| `kubectl apply -f pod.yaml` | Create/update pod from file |
| `kubectl replace --force -f pod.yaml` | Replace pod (delete and recreate) |

### Pod Operations

| Command | Description |
|---------|-------------|
| `kubectl exec <pod-name> -- <command>` | Execute command in pod |
| `kubectl exec -it <pod-name> -- /bin/bash` | Interactive shell in pod |
| `kubectl exec -it <pod-name> -c <container> -- /bin/sh` | Shell into specific container |
| `kubectl logs <pod-name>` | View pod logs |
| `kubectl logs <pod-name> -f` | Follow/stream pod logs |
| `kubectl logs <pod-name> --previous` | Logs from previous container instance |
| `kubectl logs <pod-name> -c <container>` | Logs from specific container |
| `kubectl logs <pod-name> --tail=100` | Show last 100 lines |
| `kubectl logs <pod-name> --since=1h` | Show logs from last hour |
| `kubectl logs <pod-name> --timestamps` | Show logs with timestamps |
| `kubectl logs -l <label-selector>` | Logs from all pods matching label |
| `kubectl port-forward <pod-name> 8080:80` | Forward local port 8080 to pod port 80 |
| `kubectl port-forward <pod-name> :80` | Forward random local port to pod port 80 |
| `kubectl attach <pod-name>` | Attach to running container |
| `kubectl cp <pod-name>:/path/to/file ./local-file` | Copy file from pod |
| `kubectl cp ./local-file <pod-name>:/path/to/file` | Copy file to pod |

### Labels and Selectors

| Command | Description |
|---------|-------------|
| `kubectl label pods <pod-name> env=prod` | Add label to pod |
| `kubectl label pods <pod-name> env=dev --overwrite` | Update existing label |
| `kubectl label pods <pod-name> env-` | Remove label from pod |
| `kubectl get pods -l env=prod` | Get pods with label env=prod |
| `kubectl get pods -l 'env in (prod,staging)'` | Multiple values selector |
| `kubectl get pods -l env!=prod` | Not equal selector |
| `kubectl get pods -l app,env` | Pods with both labels |
| `kubectl get pods -l 'app,!env'` | Pods with app but not env label |
| `kubectl label --all pods status=reviewed` | Label all pods |

### Annotations

| Command | Description |
|---------|-------------|
| `kubectl annotate pods <pod-name> description='My app'` | Add annotation |
| `kubectl annotate pods <pod-name> description-` | Remove annotation |
| `kubectl describe pod <pod-name> | grep Annotations` | View annotations |

---

## 🚀 Workload Resources

---

## 🚀 Workload Resources

### Deployments

| Command | Description |
|---------|-------------|
| `kubectl get deployments` | List all deployments |
| `kubectl get deploy` | List deployments (short) |
| `kubectl get deployments -o wide` | List with additional details |
| `kubectl describe deployment <name>` | Show deployment details |
| `kubectl create deployment <name> --image=<image>` | Create deployment |
| `kubectl create deployment <name> --image=<image> --replicas=3` | Create with replicas |
| `kubectl create deployment <name> --image=<image> --dry-run=client -o yaml` | Generate YAML |
| `kubectl apply -f deployment.yaml` | Create/update from file |
| `kubectl delete deployment <name>` | Delete deployment |
| `kubectl edit deployment <name>` | Edit deployment |
| `kubectl get deployment <name> -o yaml` | Get deployment YAML |

### Deployment Scaling

| Command | Description |
|---------|-------------|
| `kubectl scale deployment <name> --replicas=5` | Scale deployment to 5 replicas |
| `kubectl autoscale deployment <name> --min=2 --max=10 --cpu-percent=80` | Auto-scale deployment |
| `kubectl get hpa` | List horizontal pod autoscalers |

### Deployment Updates & Rollouts

| Command | Description |
|---------|-------------|
| `kubectl set image deployment/<name> <container>=<image>:<tag>` | Update container image |
| `kubectl set image deployment/<name> *=<image>:<tag>` | Update all containers |
| `kubectl rollout status deployment/<name>` | Check rollout status |
| `kubectl rollout history deployment/<name>` | View rollout history |
| `kubectl rollout history deployment/<name> --revision=2` | View specific revision |
| `kubectl rollout undo deployment/<name>` | Rollback to previous revision |
| `kubectl rollout undo deployment/<name> --to-revision=2` | Rollback to specific revision |
| `kubectl rollout restart deployment/<name>` | Restart deployment (rolling restart) |
| `kubectl rollout pause deployment/<name>` | Pause deployment rollout |
| `kubectl rollout resume deployment/<name>` | Resume paused deployment |
| `kubectl patch deployment <name> -p '{"spec":{"replicas":3}}'` | Patch deployment |

### ReplicaSets

| Command | Description |
|---------|-------------|
| `kubectl get replicasets` | List all ReplicaSets |
| `kubectl get rs` | List ReplicaSets (short) |
| `kubectl describe rs <name>` | Show ReplicaSet details |
| `kubectl delete rs <name>` | Delete ReplicaSet |
| `kubectl scale rs <name> --replicas=5` | Scale ReplicaSet |
| `kubectl get rs --show-labels` | Show ReplicaSet labels |

### StatefulSets

| Command | Description |
|---------|-------------|
| `kubectl get statefulsets` | List StatefulSets |
| `kubectl get sts` | List StatefulSets (short) |
| `kubectl describe sts <name>` | Show StatefulSet details |
| `kubectl create -f statefulset.yaml` | Create StatefulSet |
| `kubectl delete sts <name>` | Delete StatefulSet |
| `kubectl delete sts <name> --cascade=orphan` | Delete but keep pods |
| `kubectl scale sts <name> --replicas=5` | Scale StatefulSet |
| `kubectl patch sts <name> -p '{"spec":{"updateStrategy":{"type":"RollingUpdate"}}}'` | Change update strategy |
| `kubectl rollout status sts/<name>` | Check StatefulSet rollout status |

### DaemonSets

| Command | Description |
|---------|-------------|
| `kubectl get daemonsets` | List DaemonSets |
| `kubectl get ds` | List DaemonSets (short) |
| `kubectl describe ds <name>` | Show DaemonSet details |
| `kubectl create -f daemonset.yaml` | Create DaemonSet |
| `kubectl delete ds <name>` | Delete DaemonSet |
| `kubectl rollout status ds/<name>` | Check DaemonSet rollout status |
| `kubectl set image ds/<name> <container>=<image>` | Update DaemonSet image |

### Jobs

| Command | Description |
|---------|-------------|
| `kubectl get jobs` | List all jobs |
| `kubectl describe job <name>` | Show job details |
| `kubectl create job <name> --image=<image>` | Create job |
| `kubectl create job <name> --image=<image> --dry-run=client -o yaml` | Generate job YAML |
| `kubectl create job <name> --from=cronjob/<cron-name>` | Create job from CronJob |
| `kubectl delete job <name>` | Delete job |
| `kubectl logs job/<name>` | View job logs |
| `kubectl get pods --selector=job-name=<name>` | Get pods for job |
| `kubectl wait --for=condition=complete job/<name>` | Wait for job completion |
| `kubectl wait --for=condition=complete --timeout=60s job/<name>` | Wait with timeout |

### CronJobs

| Command | Description |
|---------|-------------|
| `kubectl get cronjobs` | List all CronJobs |
| `kubectl get cj` | List CronJobs (short) |
| `kubectl describe cronjob <name>` | Show CronJob details |
| `kubectl create cronjob <name> --image=<image> --schedule="*/5 * * * *"` | Create CronJob |
| `kubectl create cronjob <name> --image=<image> --schedule="@hourly"` | Create with named schedule |
| `kubectl delete cronjob <name>` | Delete CronJob |
| `kubectl patch cronjob <name> -p '{"spec":{"suspend":true}}'` | Suspend CronJob |
| `kubectl patch cronjob <name> -p '{"spec":{"suspend":false}}'` | Resume CronJob |
| `kubectl get jobs --watch` | Watch jobs created by CronJob |

---

## 🌐 Services & Networking

---

## 🌐 Services & Networking

### Services

| Command | Description |
|---------|-------------|
| `kubectl get services` | List all services |
| `kubectl get svc` | List services (short) |
| `kubectl get svc -o wide` | List services with details |
| `kubectl describe service <name>` | Show service details |
| `kubectl get endpoints` | List service endpoints |
| `kubectl get ep <service-name>` | Get endpoints for service |
| `kubectl create service clusterip <name> --tcp=80:8080` | Create ClusterIP service |
| `kubectl create service nodeport <name> --tcp=80:8080` | Create NodePort service |
| `kubectl create service loadbalancer <name> --tcp=80:8080` | Create LoadBalancer service |
| `kubectl expose deployment <name> --port=80 --target-port=8080` | Expose deployment as service |
| `kubectl expose pod <name> --port=80 --target-port=8080 --type=NodePort` | Expose pod as NodePort |
| `kubectl expose deployment <name> --type=LoadBalancer --port=80` | Expose as LoadBalancer |
| `kubectl delete service <name>` | Delete service |
| `kubectl edit service <name>` | Edit service |
| `kubectl get svc <name> -o yaml` | Get service YAML |
| `kubectl patch svc <name> -p '{"spec":{"type":"NodePort"}}'` | Change service type |

### Ingress

| Command | Description |
|---------|-------------|
| `kubectl get ingress` | List all ingress resources |
| `kubectl get ing` | List ingress (short) |
| `kubectl describe ingress <name>` | Show ingress details |
| `kubectl create ingress <name> --rule="host/path=service:port"` | Create ingress |
| `kubectl create ingress <name> --class=nginx --rule="example.com/*=web:80"` | Create with ingress class |
| `kubectl delete ingress <name>` | Delete ingress |
| `kubectl edit ingress <name>` | Edit ingress |
| `kubectl get ingressclass` | List ingress classes |

### Network Policies

| Command | Description |
|---------|-------------|
| `kubectl get networkpolicies` | List network policies |
| `kubectl get netpol` | List network policies (short) |
| `kubectl describe networkpolicy <name>` | Show network policy details |
| `kubectl create -f networkpolicy.yaml` | Create network policy |
| `kubectl delete networkpolicy <name>` | Delete network policy |
| `kubectl get networkpolicy <name> -o yaml` | Get network policy YAML |

### DNS & Service Discovery

| Command | Description |
|---------|-------------|
| `kubectl get svc -n kube-system` | View CoreDNS service |
| `kubectl get pods -n kube-system -l k8s-app=kube-dns` | View DNS pods |
| `kubectl exec -it <pod> -- nslookup <service-name>` | Test DNS resolution |
| `kubectl exec -it <pod> -- nslookup <service>.<namespace>.svc.cluster.local` | Full DNS lookup |
| `kubectl run -it --rm debug --image=busybox --restart=Never -- sh` | Debug pod for testing |

---

## 💾 Storage

### Persistent Volumes (PV)

| Command | Description |
|---------|-------------|
| `kubectl get persistentvolumes` | List all persistent volumes |
| `kubectl get pv` | List PVs (short) |
| `kubectl describe pv <name>` | Show PV details |
| `kubectl create -f pv.yaml` | Create persistent volume |
| `kubectl delete pv <name>` | Delete persistent volume |
| `kubectl get pv --sort-by=.spec.capacity.storage` | Sort PVs by capacity |
| `kubectl get pv -o custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage,STATUS:.status.phase` | Custom columns |

### Persistent Volume Claims (PVC)

| Command | Description |
|---------|-------------|
| `kubectl get persistentvolumeclaims` | List all PVCs |
| `kubectl get pvc` | List PVCs (short) |
| `kubectl get pvc -A` | List PVCs in all namespaces |
| `kubectl describe pvc <name>` | Show PVC details |
| `kubectl create -f pvc.yaml` | Create PVC |
| `kubectl delete pvc <name>` | Delete PVC |
| `kubectl get pvc <name> -o yaml` | Get PVC YAML |
| `kubectl patch pvc <name> -p '{"spec":{"resources":{"requests":{"storage":"10Gi"}}}}'` | Expand PVC |

### Storage Classes

| Command | Description |
|---------|-------------|
| `kubectl get storageclasses` | List storage classes |
| `kubectl get sc` | List storage classes (short) |
| `kubectl describe storageclass <name>` | Show storage class details |
| `kubectl create -f storageclass.yaml` | Create storage class |
| `kubectl delete storageclass <name>` | Delete storage class |
| `kubectl get sc <name> -o yaml` | Get storage class YAML |
| `kubectl patch storageclass <name> -p '{"metadata":{"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` | Set as default |

### Volume Snapshots

| Command | Description |
|---------|-------------|
| `kubectl get volumesnapshots` | List volume snapshots |
| `kubectl get volumesnapshotclasses` | List snapshot classes |
| `kubectl describe volumesnapshot <name>` | Show snapshot details |
| `kubectl create -f snapshot.yaml` | Create volume snapshot |
| `kubectl delete volumesnapshot <name>` | Delete snapshot |

---

## ⚙️ Configuration

### ConfigMaps

| Command | Description |
|---------|-------------|
| `kubectl get configmaps` | List all ConfigMaps |
| `kubectl get cm` | List ConfigMaps (short) |
| `kubectl describe configmap <name>` | Show ConfigMap details |
| `kubectl create configmap <name> --from-file=<path>` | Create from file |
| `kubectl create configmap <name> --from-file=<key>=<path>` | Create with custom key |
| `kubectl create configmap <name> --from-literal=<key>=<value>` | Create from literal |
| `kubectl create configmap <name> --from-env-file=<path>` | Create from env file |
| `kubectl create configmap <name> --from-file=dir/` | Create from directory |
| `kubectl create configmap <name> --dry-run=client -o yaml` | Generate YAML |
| `kubectl delete configmap <name>` | Delete ConfigMap |
| `kubectl edit configmap <name>` | Edit ConfigMap |
| `kubectl get configmap <name> -o yaml` | Get ConfigMap YAML |
| `kubectl get configmap <name> -o jsonpath='{.data}'` | Get ConfigMap data |

### Secrets

| Command | Description |
|---------|-------------|
| `kubectl get secrets` | List all secrets |
| `kubectl describe secret <name>` | Show secret details |
| `kubectl create secret generic <name> --from-literal=<key>=<value>` | Create generic secret |
| `kubectl create secret generic <name> --from-file=<path>` | Create from file |
| `kubectl create secret generic <name> --from-file=<key>=<path>` | Create with custom key |
| `kubectl create secret generic <name> --from-env-file=<path>` | Create from env file |
| `kubectl create secret docker-registry <name> --docker-server=<server> --docker-username=<user> --docker-password=<pwd>` | Docker registry secret |
| `kubectl create secret tls <name> --cert=<cert-file> --key=<key-file>` | TLS secret |
| `kubectl delete secret <name>` | Delete secret |
| `kubectl get secret <name> -o yaml` | Get secret YAML |
| `kubectl get secret <name> -o jsonpath='{.data}'` | Get secret data (base64) |
| `kubectl get secret <name> -o jsonpath='{.data.password}' \| base64 -d` | Decode secret value |
| `echo -n 'mypassword' \| base64` | Encode value for secret |

### Resource Quotas

| Command | Description |
|---------|-------------|
| `kubectl get resourcequotas` | List resource quotas |
| `kubectl get quota` | List quotas (short) |
| `kubectl describe resourcequota <name>` | Show quota details |
| `kubectl create -f quota.yaml` | Create resource quota |
| `kubectl delete resourcequota <name>` | Delete quota |

### Limit Ranges

| Command | Description |
|---------|-------------|
| `kubectl get limitranges` | List limit ranges |
| `kubectl get limits` | List limits (short) |
| `kubectl describe limitrange <name>` | Show limit range details |
| `kubectl create -f limitrange.yaml` | Create limit range |
| `kubectl delete limitrange <name>` | Delete limit range |

### Service Accounts

| Command | Description |
|---------|-------------|
| `kubectl get serviceaccounts` | List service accounts |
| `kubectl get sa` | List service accounts (short) |
| `kubectl describe serviceaccount <name>` | Show service account details |
| `kubectl create serviceaccount <name>` | Create service account |
| `kubectl delete serviceaccount <name>` | Delete service account |
| `kubectl get sa <name> -o yaml` | Get service account YAML |
| `kubectl create token <serviceaccount-name>` | Create token for service account |

---

## 🔐 RBAC & Security

### Roles and RoleBindings

| Command | Description |
|---------|-------------|
| `kubectl get roles` | List roles in current namespace |
| `kubectl get roles -A` | List roles in all namespaces |
| `kubectl describe role <name>` | Show role details |
| `kubectl create role <name> --verb=get,list --resource=pods` | Create role |
| `kubectl create role <name> --verb=* --resource=*.*` | Create role with all permissions |
| `kubectl delete role <name>` | Delete role |
| `kubectl get rolebindings` | List role bindings |
| `kubectl describe rolebinding <name>` | Show role binding details |
| `kubectl create rolebinding <name> --role=<role> --user=<user>` | Bind role to user |
| `kubectl create rolebinding <name> --role=<role> --serviceaccount=<ns>:<sa>` | Bind role to service account |
| `kubectl delete rolebinding <name>` | Delete role binding |

### ClusterRoles and ClusterRoleBindings

| Command | Description |
|---------|-------------|
| `kubectl get clusterroles` | List cluster roles |
| `kubectl describe clusterrole <name>` | Show cluster role details |
| `kubectl create clusterrole <name> --verb=get,list --resource=pods` | Create cluster role |
| `kubectl delete clusterrole <name>` | Delete cluster role |
| `kubectl get clusterrolebindings` | List cluster role bindings |
| `kubectl describe clusterrolebinding <name>` | Show cluster role binding details |
| `kubectl create clusterrolebinding <name> --clusterrole=<role> --user=<user>` | Bind cluster role to user |
| `kubectl create clusterrolebinding <name> --clusterrole=<role> --serviceaccount=<ns>:<sa>` | Bind to service account |
| `kubectl delete clusterrolebinding <name>` | Delete cluster role binding |

### Authorization Testing

| Command | Description |
|---------|-------------|
| `kubectl auth can-i <verb> <resource>` | Check if you can perform action |
| `kubectl auth can-i create deployments` | Check if you can create deployments |
| `kubectl auth can-i '*' '*'` | Check if you have all permissions |
| `kubectl auth can-i get pods --as=<user>` | Check permissions as another user |
| `kubectl auth can-i get pods --as=system:serviceaccount:<ns>:<sa>` | Check as service account |
| `kubectl auth can-i get pods -n <namespace>` | Check in specific namespace |

### Pod Security

| Command | Description |
|---------|-------------|
| `kubectl label namespace <name> pod-security.kubernetes.io/enforce=baseline` | Set pod security standard |
| `kubectl label namespace <name> pod-security.kubernetes.io/enforce=restricted` | Enforce restricted policy |
| `kubectl label namespace <name> pod-security.kubernetes.io/warn=baseline` | Set warning mode |
| `kubectl label namespace <name> pod-security.kubernetes.io/audit=restricted` | Set audit mode |

---

## 📊 Monitoring & Debugging

### Cluster Events

| Command | Description |
|---------|-------------|
| `kubectl get events` | List events in current namespace |
| `kubectl get events -A` | List events in all namespaces |
| `kubectl get events --sort-by=.metadata.creationTimestamp` | Sort events by time |
| `kubectl get events --field-selector type=Warning` | Filter warning events |
| `kubectl get events --field-selector involvedObject.name=<pod>` | Events for specific pod |
| `kubectl get events --watch` | Watch events in real-time |

### Resource Usage

| Command | Description |
|---------|-------------|
| `kubectl top nodes` | Show node resource usage (CPU/Memory) |
| `kubectl top pods` | Show pod resource usage |
| `kubectl top pods -A` | Show pod usage in all namespaces |
| `kubectl top pods --containers` | Show usage by container |
| `kubectl top pods -l <label>` | Show usage for labeled pods |
| `kubectl top pods --sort-by=cpu` | Sort pods by CPU usage |
| `kubectl top pods --sort-by=memory` | Sort pods by memory usage |

### Debugging Pods

| Command | Description |
|---------|-------------|
| `kubectl describe pod <pod-name>` | Detailed pod information and events |
| `kubectl get pod <pod-name> -o yaml` | Full pod specification |
| `kubectl get pod <pod-name> -o jsonpath='{.status.phase}'` | Get pod phase |
| `kubectl get pods --field-selector status.phase=Pending` | List pending pods |
| `kubectl get pods --field-selector status.phase=Failed` | List failed pods |
| `kubectl debug pod/<pod-name> -it --image=busybox` | Debug with ephemeral container |
| `kubectl debug node/<node-name> -it --image=ubuntu` | Debug node |
| `kubectl run debug --image=busybox -it --rm --restart=Never -- sh` | Temporary debug pod |

### Debugging Services

| Command | Description |
|---------|-------------|
| `kubectl describe service <name>` | Service details and events |
| `kubectl get endpoints <service-name>` | Check service endpoints |
| `kubectl run tmp-shell --image=nicolaka/netshoot -it --rm` | Network debug pod |
| `kubectl exec -it <pod> -- wget -O- <service-name>` | Test service connectivity |

### Cluster Troubleshooting

| Command | Description |
|---------|-------------|
| `kubectl get componentstatuses` | Check control plane component status |
| `kubectl get cs` | Component status (short) |
| `kubectl get --raw /healthz` | API server health |
| `kubectl get --raw /readyz` | API server readiness |
| `kubectl get --raw /livez` | API server liveness |

### Node Operations

| Command | Description |
|---------|-------------|
| `kubectl get nodes` | List all nodes |
| `kubectl get nodes -o wide` | List nodes with additional details |
| `kubectl describe node <node-name>` | Node details and conditions |
| `kubectl cordon <node-name>` | Mark node as unschedulable |
| `kubectl uncordon <node-name>` | Mark node as schedulable |
| `kubectl drain <node-name>` | Drain node (evict pods for maintenance) |
| `kubectl drain <node-name> --ignore-daemonsets` | Drain while keeping DaemonSets |
| `kubectl drain <node-name> --force --delete-emptydir-data` | Force drain with local data |
| `kubectl taint nodes <node-name> key=value:NoSchedule` | Add taint to node |
| `kubectl taint nodes <node-name> key:NoSchedule-` | Remove taint from node |
| `kubectl label nodes <node-name> <label-key>=<label-value>` | Add label to node |

---

## 🔧 Advanced Operations

### Scheduling

| Command | Description |
|---------|-------------|
| `kubectl apply -f <file.yaml>` | Apply configuration from file |
| `kubectl apply -f <directory>` | Apply all files in directory |
| `kubectl delete -f <file.yaml>` | Delete resources from file |
| `kubectl edit <resource> <name>` | Edit resource |
| `kubectl get <resource> -o yaml` | Get resource as YAML |
| `kubectl get <resource> -o json` | Get resource as JSON |

### Labels & Annotations

| Command | Description |
|---------|-------------|
| `kubectl label pods <pod-name> env=prod` | Add label to pod |
| `kubectl label pods <pod-name> env-` | Remove label from pod |
| `kubectl get pods -l env=prod` | List pods by label |
| `kubectl annotate pods <pod-name> description='my app'` | Add annotation |

### Debugging

| Command | Description |
|---------|-------------|
| `kubectl get events` | List cluster events |
| `kubectl get events --sort-by=.metadata.creationTimestamp` | Sorted events |
| `kubectl top pods` | Show pod resource usage |
| `kubectl top nodes` | Show node resource usage |
| `kubectl describe pod <pod-name>` | Debug pod issues |
| `kubectl logs <pod-name> --previous` | Logs from crashed container |

### Other Resources


---

## 🔧 Advanced Operations

### Scheduling

| Command | Description |
|---------|-------------|
| `kubectl get pods -o wide --sort-by=.spec.nodeName` | View pod distribution across nodes |
| `kubectl get pods --field-selector spec.nodeName=<node-name>` | Pods on specific node |
| `kubectl get priorityclasses` | List priority classes |
| `kubectl describe priorityclass <name>` | Show priority class details |

### Resource Patching

| Command | Description |
|---------|-------------|
| `kubectl patch pod <name> -p '{"spec":{"containers":[{"name":"app","image":"new-image"}]}}'` | Patch pod (JSON) |
| `kubectl patch deployment <name> --type='json' -p='[{"op":"replace","path":"/spec/replicas","value":5}]'` | JSON patch |
| `kubectl patch svc <name> -p '{"spec":{"type":"NodePort"}}'` | Change service type |
| `kubectl set image deployment/<name> <container>=<image>:<tag>` | Update image |
| `kubectl set resources deployment/<name> -c=<container> --limits=cpu=200m,memory=512Mi` | Set resource limits |
| `kubectl set env deployment/<name> KEY=value` | Set environment variable |
| `kubectl set serviceaccount deployment/<name> <sa-name>` | Set service account |

### JSONPath & Custom Columns

| Command | Description |
|---------|-------------|
| `kubectl get pods -o jsonpath='{.items[*].metadata.name}'` | List pod names |
| `kubectl get pods -o jsonpath='{.items[*].status.podIP}'` | List pod IPs |
| `kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}'` | Node IPs |
| `kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase` | Custom columns |
| `kubectl get pods -o custom-columns=POD:.metadata.name,NODE:.spec.nodeName,IP:.status.podIP` | Multiple columns |
| `kubectl get pv -o custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage,STATUS:.status.phase` | PV info |

### Cluster Management

| Command | Description |
|---------|-------------|
| `kubectl apply -f <file.yaml>` | Apply configuration from file |
| `kubectl apply -f <directory>/` | Apply all YAML files in directory |
| `kubectl apply -f <url>` | Apply from URL |
| `kubectl apply -k <directory>` | Apply kustomization |
| `kubectl delete -f <file.yaml>` | Delete resources from file |
| `kubectl diff -f <file.yaml>` | Show diff before applying |
| `kubectl replace -f <file.yaml>` | Replace resource |
| `kubectl replace --force -f <file.yaml>` | Force replace (delete and recreate) |
| `kubectl wait --for=condition=ready pod -l app=myapp` | Wait for condition |
| `kubectl wait --for=delete pod/<pod-name> --timeout=60s` | Wait for deletion |

### Resource Conversion & Generation

| Command | Description |
|---------|-------------|
| `kubectl create deployment <name> --image=<image> --dry-run=client -o yaml > deploy.yaml` | Generate deployment YAML |
| `kubectl create service clusterip <name> --tcp=80:8080 --dry-run=client -o yaml` | Generate service YAML |
| `kubectl run <pod> --image=<image> --dry-run=client -o yaml` | Generate pod YAML |
| `kubectl create configmap <name> --from-literal=key=val --dry-run=client -o yaml` | Generate ConfigMap YAML |
| `kubectl create secret generic <name> --from-literal=key=val --dry-run=client -o yaml` | Generate secret YAML |
| `kubectl get pod <pod> -o yaml --export` | Export resource (deprecated) |
| `kubectl convert -f <old-file.yaml> --output-version <new-api>` | Convert API version |

### Plugin Management (Krew)

| Command | Description |
|---------|-------------|
| `kubectl krew install <plugin>` | Install kubectl plugin |
| `kubectl krew list` | List installed plugins |
| `kubectl krew update` | Update plugin index |
| `kubectl krew upgrade` | Upgrade installed plugins |
| `kubectl krew search` | Search available plugins |

### Useful Plugins

| Plugin | Command | Description |
|--------|---------|-------------|
| ctx | `kubectl ctx` | Switch contexts easily |
| ns | `kubectl ns` | Switch namespaces easily |
| tree | `kubectl tree <resource> <name>` | Show resource hierarchy |
| who-can | `kubectl who-can <verb> <resource>` | Show who has RBAC permissions |
| node-shell | `kubectl node-shell <node>` | Shell into node |
| tail | `kubectl tail <pod>` | Multi-pod log tailing |

---

## 🛠️ Kubectl Shortcuts & Aliases

Add these to your `~/.bashrc` or `~/.zshrc`:

```bash
# Kubectl alias
alias k='kubectl'
alias kc='kubectl'

# Common operations
alias kgp='kubectl get pods'
alias kgd='kubectl get deployments'
alias kgs='kubectl get services'
alias kgn='kubectl get nodes'
alias kga='kubectl get all'

# With all namespaces
alias kgpa='kubectl get pods -A'
alias kgda='kubectl get deployments -A'
alias kgsa='kubectl get services -A'

# Wide output
alias kgpw='kubectl get pods -o wide'
alias kgdw='kubectl get deployments -o wide'

# Describe
alias kdp='kubectl describe pod'
alias kdd='kubectl describe deployment'
alias kds='kubectl describe service'
alias kdn='kubectl describe node'

# Logs
alias kl='kubectl logs'
alias klf='kubectl logs -f'
alias klp='kubectl logs --previous'

# Execute
alias kex='kubectl exec -it'
alias keti='kubectl exec -it'

# Apply and delete
alias ka='kubectl apply -f'
alias kdel='kubectl delete -f'
alias kaf='kubectl apply -f'
alias kdf='kubectl delete -f'

# Context and namespace
alias kctx='kubectl config current-context'
alias kcon='kubectl config use-context'
alias kns='kubectl config set-context --current --namespace'

# Edit
alias ke='kubectl edit'
alias kep='kubectl edit pod'
alias ked='kubectl edit deployment'

# Port forward
alias kpf='kubectl port-forward'

# Scale
alias kscale='kubectl scale deployment'

# Rollout
alias kroll='kubectl rollout'
alias krollr='kubectl rollout restart'
alias krollu='kubectl rollout undo'
alias krolls='kubectl rollout status'

# Top
alias ktop='kubectl top'
alias ktopn='kubectl top nodes'
alias ktopp='kubectl top pods'
```

---

## 💡 Pro Tips

### Speed Tips
- Use `kubectl` autocomplete: `source <(kubectl completion bash)` or `source <(kubectl completion zsh)`
- Use `-o wide` for more details in output
- Use `--dry-run=client -o yaml` to generate YAML templates
- Use `kubectl explain <resource>` for built-in documentation
- Use short names: `po` (pods), `svc` (services), `deploy` (deployments), `ns` (namespaces)

### Debugging Tips
- Check events first: `kubectl get events --sort-by=.metadata.creationTimestamp`
- Use `describe` for detailed troubleshooting
- Check logs with `--previous` for crashed containers
- Use `kubectl debug` for ephemeral containers
- Use `kubectl explain <resource>.spec` to understand fields

### YAML Generation
- Always use `--dry-run=client -o yaml > file.yaml` to generate templates
- Edit generated YAML before applying
- Use `kubectl diff -f file.yaml` before applying changes
- Validate YAML with `kubectl apply --dry-run=client -f file.yaml`

### Resource Management
- Always specify resource requests and limits
- Use namespaces to organize resources
- Use labels for filtering and selection
- Set resource quotas per namespace
- Use limit ranges to enforce defaults

---

**Last Updated**: January 2026
