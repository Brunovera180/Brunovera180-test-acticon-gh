# Comandos Básicos para la Administración de Amazon EKS

Este documento proporciona una lista de comandos básicos para la administración de clústeres de **Amazon EKS** (Elastic Kubernetes Service). Incluye operaciones como crear, administrar, actualizar, eliminar nodos y otras tareas comunes.

## Configuración Inicial

### Configurar AWS CLI
Antes de ejecutar cualquier comando de EKS, debes configurar tu entorno con las credenciales de AWS.

```bash
aws configure
```

Configurar acceso al clúster EKS
Para acceder a tu clúster de EKS con kubectl, debes actualizar el archivo kubeconfig:
```bash
aws eks --region <region> update-kubeconfig --name <cluster-name>
```

## Comandos para la Administración de EKS
### Ver información sobre el clúster
Listar todos los clústeres EKS:
```bash
eksctl get cluster
```

Describir un clúster específico:
```bash
eksctl get cluster --name <cluster-name>
```

Obtener detalles de un nodo del clúster:
```bash
kubectl describe nodes
```

### Crear y eliminar clústeres
Crear un clúster usando un archivo YAML:
```bash
eksctl create cluster -f <cluster-config.yaml>
```

Eliminar un clúster:
```bash
eksctl delete cluster --name <cluster-name>
```

### Administración de grupos de nodos (Node Groups)
Listar los grupos de nodos del clúster:
```bash
eksctl get nodegroup --cluster <cluster-name>
```

Crear un grupo de nodos:
```bash
eksctl create nodegroup --cluster <cluster-name> --name <nodegroup-name> --nodes 3 --node-type t2.medium
```

Eliminar un grupo de nodos:
```bash
eksctl delete nodegroup --cluster <cluster-name> --name <nodegroup-name>
```

### Actualizar clústeres y nodos
Actualizar la versión de Kubernetes en el clúster:
```bash
eksctl upgrade cluster --name <cluster-name> --approve
```
Actualizar un grupo de nodos a una nueva versión de Kubernetes:
```bash
eksctl upgrade nodegroup --cluster <cluster-name> --name <nodegroup-name>
```

### Administración de pods y recursos de Kubernetes
Listar todos los pods en un namespace:
```bash
kubectl get pods -n <namespace>
```

Ver los servicios en un namespace:
```bash
kubectl get svc -n <namespace>
```

Describir un pod específico:
```bash
kubectl describe pod <pod-name> -n <namespace>
```

Reiniciar un pod:
```bash
kubectl delete pod <pod-name> -n <namespace>
```

Escalar un deployment:
```bash
kubectl scale deployment <deployment-name> --replicas=<número-replicas> -n <namespace>
```

### Manejo de logs
Ver los logs de un pod específico:
```bash
kubectl logs <pod-name> -n <namespace>
```

Ver los logs en tiempo real de un pod:
```bash
kubectl logs -f <pod-name> -n <namespace>
```

### Monitoreo y métricas
Ver las métricas de los pods:
```bash
kubectl top pods -n <namespace>
```

Ver las métricas de los nodos:
```bash
kubectl top nodes
```

### Gestionar accesos (RBAC)
Ver los roles disponibles:
```bash
kubectl get roles -n <namespace>
```

Asignar un rol a un usuario o grupo:
```bash
kubectl create rolebinding <binding-name> --role=<role-name> --user=<user-name> -n <namespace>
```

### Eliminar recursos
Eliminar un deployment:
```bash
kubectl delete deployment <deployment-name> -n <namespace>
```

Eliminar un pod específico:
```bash
kubectl delete pod <pod-name> -n <namespace>
```

Eliminar un servicio:
```bash
kubectl delete svc <service-name> -n <namespace>
```
