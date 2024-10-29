## `kubectl describe deployment dev-backend`

```bash
user@machine~/capella-collab-manager$ kubectl describe deployment dev-backend
Name:                   dev-backend
Namespace:              collab-manager
CreationTimestamp:      Tue, 29 Oct 2024 16:45:43 +0100
Labels:                 app.kubernetes.io/managed-by=Helm
                        id=dev-deployment-backend
Annotations:            checksum/config-backend: 34507fe48746744a8bf0cc7ccdb6c442ff329f8e57994baef9d0d57095b6f428
                        checksum/config-promtail: dd348929d67fcb6414b328992fde988c74864b4c06df7401e29273ddc745f3b2
                        deployment.kubernetes.io/revision: 1
                        meta.helm.sh/release-name: dev
                        meta.helm.sh/release-namespace: collab-manager
Selector:               id=dev-deployment-backend
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:           id=dev-deployment-backend
  Annotations:      checksum/config-backend: 34507fe48746744a8bf0cc7ccdb6c442ff329f8e57994baef9d0d57095b6f428
                    checksum/config-promtail: dd348929d67fcb6414b328992fde988c74864b4c06df7401e29273ddc745f3b2
  Service Account:  dev-backend
  Containers:
   dev-backend:
    Image:      ghcr.io/dsd-dbs/capella-collab-manager/backend:v4.10.0
    Port:       8000/TCP
    Host Port:  0/TCP
    Limits:
      cpu:                250m
      ephemeral-storage:  2Gi
      memory:             500Mi
    Requests:
      cpu:                60m
      ephemeral-storage:  1Gi
      memory:             20Mi
    Environment:
      OAUTHLIB_INSECURE_TRANSPORT:  1
      CLUSTER_DEVELOPMENT_MODE:     1
      no_proxy_additional:          
    Mounts:
      /.local/share/capellacollab from data (rw)
      /etc/capellacollab from config (ro)
      /var/log/backend from logs (rw)
   promtail:
    Image:      docker.io/grafana/promtail
    Port:       3101/TCP
    Host Port:  0/TCP
    Args:
      --config.file=/etc/promtail/promtail.yaml
      -log-config-reverse-order
    Limits:
      cpu:                100m
      ephemeral-storage:  2Gi
      memory:             50Mi
    Requests:
      cpu:                20m
      ephemeral-storage:  1Gi
      memory:             5Mi
    Environment:          <none>
    Mounts:
      /etc/promtail from prom-config (rw)
      /var/log/backend from logs (ro)
      /var/log/promtail from prom-position (rw)
  Volumes:
   config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      dev-backend
    Optional:  false
   data:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  dev-backend-data
    ReadOnly:   false
   logs:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
   prom-config:
    Type:      ConfigMap (a volume populated by a ConfigMap)
    Name:      dev-promtail
    Optional:  false
   prom-position:
    Type:          PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:     dev-backend-promtail
    ReadOnly:      false
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   dev-backend-649d7964c9 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  34m   deployment-controller  Scaled up replica set dev-backend-649d7964c9 to 1
```