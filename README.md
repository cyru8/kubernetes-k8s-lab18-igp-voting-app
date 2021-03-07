# kubenetes-k8s-lab02
# kubectl create or apply -f deployment.yaml
# automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl get deployment
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
webapp01   0/1     1            0           17s


automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl describe deployment webapp01
Name:                   webapp01
Namespace:              default
CreationTimestamp:      Thu, 25 Feb 2021 23:08:02 -0800
Labels:                 app=webapps
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=webapps
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=webapps
  Containers:
   webapp01:
    Image:      katacoda/docker-http-server:latest
    Port:       80/TCP
    Host Port:  0/TCP
    Limits:
      cpu:     100m
      memory:  100Mi
    Requests:
      cpu:        100m
      memory:     100Mi
    Liveness:     tcp-socket :80 delay=5s timeout=5s period=10s #success=1 #failure=3
    Readiness:    http-get http://:80/_status/healthz delay=5s timeout=2s period=10s #success=1 #failure=3
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   webapp01-6b8f85d6cc (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  70s   deployment-controller  Scaled up replica set webapp01-6b8f85d6cc to 1


automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl apply -f service.yaml 
service/webapps-svc created

automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl get svc webapps-svc -o wide
NAME          TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE   SELECTOR
webapps-svc   NodePort   10.110.137.247   <none>        80:30080/TCP   94s   app=webapps
automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ 


automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl describe svc webapps-svc
Name:                     webapps-svc
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=webapps
Type:                     NodePort
IP Families:              <none>
IP:                       10.110.137.247
IPs:                      10.110.137.247
Port:                     webapps  80/TCP
TargetPort:               80/TCP
NodePort:                 webapps  30080/TCP
Endpoints:                10.244.104.12:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ 

$ curl node2:30080


automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl get pods
NAME                        READY   STATUS              RESTARTS   AGE
webapp01-6b8f85d6cc-57hhn   0/1     ContainerCreating   0          16s
webapp01-6b8f85d6cc-7wz5r   0/1     ContainerCreating   0          16s
webapp01-6b8f85d6cc-fc2qq   1/1     Running             0          23m
webapp01-6b8f85d6cc-jrn9n   0/1     ContainerCreating   0          16s
automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ 


utomationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ kubectl get pods -o wide
NAME                        READY   STATUS              RESTARTS   AGE   IP              NODE    NOMINATED NODE   READINESS GATES
webapp01-6b8f85d6cc-57hhn   1/1     Running             0          37s   10.244.104.13   node2   <none>           <none>
webapp01-6b8f85d6cc-7wz5r   1/1     Running             0          37s   10.244.104.14   node2   <none>           <none>
webapp01-6b8f85d6cc-fc2qq   1/1     Running             0          23m   10.244.104.12   node2   <none>           <none>
webapp01-6b8f85d6cc-jrn9n   0/1     ContainerCreating   0          37s   <none>          node1   <none>           <none>
automationmgr@master1:~/workbench/kubenetesbench/kubenetes-k8s-lab02$ 
# kubernetes-k8s-lab18-igp-voting-app
# kubernetes-k8s-lab18-igp-voting-app
# kubernetes-k8s-lab18-igp-voting-app
