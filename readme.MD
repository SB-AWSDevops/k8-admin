## Here is a simplified high-level tree format of what happens when you run kubectl get nodes in an EKS cluster:
```
kubectl get nodes
|
|-- 1. **Authentication**
|   |-- `kubectl` checks IAM credentials (from AWS CLI or IAM role).
|   |-- Authentication with Kubernetes API server using `aws-auth` ConfigMap.
|
|-- 2. **Authorization**
|   |-- API server verifies permissions via RBAC.
|   |-- `aws-auth` ConfigMap maps IAM role/user to Kubernetes groups.
|   |-- RoleBindings/ClusterRoleBindings check if user has access to nodes.
|
|-- 3. **Request Processing**
|   |-- API server receives the `get nodes` request.
|   |-- Queries etcd (Kubernetes data store) for node information.
|
|-- 4. **Response**
|   |-- API server formats and sends node information back to `kubectl`.
|
|-- 5. **Display**
|   |-- `kubectl` displays node information in your terminal.
