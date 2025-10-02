# <center>Kubernetes (K8s) Interview Questions</center>

1. ## **What is Kubernetes?**

   _Kubernetes (K8s) is an **open-source container orchestration platform** that
   automates deployment, scaling, and management of containerized applications.
   It was originally developed by Google and is now maintained by the Cloud
   Native Computing Foundation (CNCF)._

   **Key Features:**

   - **Automated Scaling:** Adjust pods dynamically with demand.
   - **Load Balancing:** Distribute traffic across pods.
   - **Self-Healing:** Restart failed pods and maintain desired state.
   - **Service Discovery:** DNS-based pod/service discovery.
   - **Storage Orchestration:** Mount cloud or on-prem storage.
   - **Rolling Updates & Rollbacks:** Zero-downtime updates.
   - **Secret and Configuration Management:** Secure management of sensitive
     data.
   - **Batch Execution:** Run batch jobs and scheduled tasks.

2. ## **Kubernetes Architecture - Detailed Breakdown**

   - **Control Plane Components:**

     - **API Server:** Frontend for Kubernetes control plane, handles REST
       operations
     - **etcd:** Consistent and highly-available key-value store for cluster
       data
     - **Controller Manager:** Runs controller processes (Node, Replication,
       Endpoints, etc.)
     - **Scheduler:** Assigns pods to nodes based on resource requirements and
       constraints
     - **Cloud Controller Manager:** Links to cloud provider APIs (optional)

   - **Worker Node Components:**

     - **Kubelet:** Agent that ensures containers are running in pods
     - **Kube Proxy:** Maintains network rules and handles packet forwarding
     - **Container Runtime:** Software that runs containers (Docker, containerd,
       CRI-O)

   - **Addons:**
     - **DNS:** Cluster DNS server (CoreDNS)
     - **Dashboard:** Web-based UI
     - **Ingress Controller:** Provides HTTP routing
     - **Network Plugins:** Implement container network interface (CNI)

3. ## **Your Experience with Kubernetes?**

   - **Cluster Setup:** On AWS EKS, GCP GKE, Azure AKS, on-prem clusters using
     kubeadm.
   - **Workloads:** Deployments, StatefulSets, DaemonSets, Jobs, CronJobs.
   - **Networking:** Ingress controllers (NGINX, Traefik), Istio service mesh,
     Calico, Flannel.
   - **Storage:** PVs, PVCs, cloud volumes (EBS, Ceph, NFS), StorageClasses.
   - **CI/CD:** GitOps (ArgoCD, Flux), Jenkins, GitHub Actions, Helm, Kustomize.
   - **Security:** RBAC, Network Policies, Pod Security Standards, OPA
     Gatekeeper.
   - **Monitoring:** Prometheus, Grafana, ELK/EFK stack, Loki, Datadog.
   - **Troubleshooting:** Pod crashes, networking issues, scaling problems,
     resource constraints.
   - **Disaster Recovery:** Backup strategies with Velero, cluster migration.

4. ## **What is a ReplicaSet?**

   _ReplicaSet ensures a **specified number of pod replicas** are running at any
   given time. It replaces the older ReplicationController._

   ```yaml
   apiVersion: apps/v1
   kind: ReplicaSet
   metadata:
     name: frontend
     labels:
       app: guestbook
       tier: frontend
   spec:
     replicas: 3
     selector:
       matchLabels:
         tier: frontend
     template:
       metadata:
         labels:
           tier: frontend
       spec:
         containers:
           - name: php-redis
             image: gcr.io/google_samples/gb-frontend:v3
   ```

   ```bash
   kubectl get rs
   kubectl scale rs my-rs --replicas=5
   kubectl describe rs <replicaset-name>
   ```

5. ## **Deployment vs StatefulSet vs DaemonSet**

   | Feature                    | Deployment                                  | StatefulSet                                       | DaemonSet                                          |
   | -------------------------- | ------------------------------------------- | ------------------------------------------------- | -------------------------------------------------- |
   | **Use Case**               | Stateless applications                      | Stateful applications (databases, clustered apps) | Cluster-wide services (logging, monitoring)        |
   | **Pod Identity**           | Random names (e.g., `app-7c8d65f7b-abc123`) | Stable, ordered names (`app-0`, `app-1`)          | Random names but node-specific                     |
   | **Pod Interchangeability** | ✅ Pods are identical and interchangeable   | ❌ Pods are unique and not interchangeable        | ✅ Pods are identical but node-bound               |
   | **Networking**             | Unstable DNS (load-balanced)                | Stable DNS (`pod-name.service-name`)              | Unstable DNS (load-balanced)                       |
   | **Storage**                | Ephemeral or shared storage                 | Persistent storage tied to pod identity           | Typically ephemeral or hostPath                    |
   | **Scaling**                | Random/parallel                             | Ordered (0, 1, 2...)                              | Automatic with node addition                       |
   | **Update Strategy**        | RollingUpdate (default) or Recreate         | RollingUpdate (ordered)                           | RollingUpdate                                      |
   | **Pod Creation**           | Parallel                                    | Sequential (0, then 1, then 2)                    | Parallel per node                                  |
   | **Pod Deletion**           | Parallel                                    | Reverse sequential (2, then 1, then 0)            | Parallel per node                                  |
   | **Storage Persistence**    | ❌ Not maintained across rescheduling       | ✅ Persistent storage follows the pod             | ❌ Not typically persistent                        |
   | **Headless Service**       | Optional                                    | Required for stable network identities            | Optional                                           |
   | **Node Affinity**          | Optional                                    | Optional                                          | ✅ Runs on all/specified nodes automatically       |
   | **Examples**               | Web servers, APIs, microservices            | MySQL, MongoDB, Elasticsearch, Kafka              | Fluentd, Prometheus Node Exporter, storage drivers |

   **YAML Examples Comparison**

   - **Stateless Deployment:**

     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: web-server
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: web
       template:
         metadata:
           labels:
             app: web
         spec:
           containers:
             - name: nginx
               image: nginx:latest
               ports:
                 - containerPort: 80
     ```

   - **StatefulSet Deployment:**

     ```yaml
     apiVersion: apps/v1
     kind: StatefulSet
     metadata:
       name: database
     spec:
       serviceName: 'database'
       replicas: 3
       selector:
         matchLabels:
           app: database
       template:
         metadata:
           labels:
             app: database
         spec:
           containers:
             - name: db
               image: mysql:8.0
               ports:
                 - containerPort: 3306
               volumeMounts:
                 - name: data
                   mountPath: /var/lib/mysql
       volumeClaimTemplates:
         - metadata:
             name: data
           spec:
             accessModes: ['ReadWriteOnce']
             resources:
               requests:
                 storage: 10Gi
     ```

   - **DaemonSet Deployment:**
     ```yaml
     apiVersion: apps/v1
     kind: DaemonSet
     metadata:
       name: log-collector
     spec:
       selector:
         matchLabels:
           app: fluentd
       template:
         metadata:
           labels:
             app: fluentd
         spec:
           containers:
             - name: fluentd
               image: fluentd:latest
               volumeMounts:
                 - name: varlog
                   mountPath: /var/log
                 - name: config
                   mountPath: /etc/fluentd
           volumes:
             - name: varlog
               hostPath:
                 path: /var/log
             - name: config
               configMap:
                 name: fluentd-config
     ```

6. ## **How does Kubernetes handle networking?**

   _Kubernetes networking follows four fundamental rules:_

   - **Pod-to-Pod communication:** All pods can communicate with all other pods
     without NAT
   - **Node-to-Pod communication:** Nodes can communicate with all pods
   - **Pod identity:** A pod sees itself the same way others see it
   - **Service discovery:** Built-in DNS for service discovery

   **Key Networking Concepts:**

   - **CNI (Container Network Interface):** Plugin architecture for networking
     (Calico, Flannel, Weave)
   - **Services:** Abstract way to expose applications
   - **Ingress:** Manages external HTTP(S) access
   - **Network Policies:** Firewall rules for pods

7. ## **What are Kubernetes Services?**

   _Services provide stable network endpoint for pods that may be ephemeral._

   **Service Types:**

   - **ClusterIP (default)**

     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-service
     spec:
       selector:
         app: MyApp
       ports:
         - protocol: TCP
           port: 80
           targetPort: 9376
     ```

   - **NodePort**

     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-service
     spec:
       type: NodePort
       selector:
         app: MyApp
       ports:
         - port: 80
           targetPort: 9376
           nodePort: 30007
     ```

   - **LoadBalancer**

     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-service
     spec:
       type: LoadBalancer
       selector:
         app: MyApp
       ports:
         - protocol: TCP
           port: 80
           targetPort: 9376
     ```

   - **ExternalName**
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: my-service
     spec:
       type: ExternalName
       externalName: my.database.example.com
     ```

8. ## **What is an Ingress?**

   _Ingress manages **external HTTP/HTTPS access** to services within the
   cluster, providing:_

   - Load balancing
   - SSL termination
   - Name-based virtual hosting
   - Path-based routing

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: my-ingress
     annotations:
       nginx.ingress.kubernetes.io/rewrite-target: /
   spec:
     tls:
       - hosts:
           - myapp.com
         secretName: myapp-tls
     rules:
       - host: myapp.com
         http:
           paths:
             - path: /
               pathType: Prefix
               backend:
                 service:
                   name: my-service
                   port:
                     number: 80
   ```

   **Popular Ingress Controllers:**

   - NGINX Ingress Controller
   - Traefik
   - HAProxy
   - Istio Gateway
   - AWS ALB Ingress Controller

9. ## **How does Kubernetes handle storage?**

   **Storage Concepts:**

   - **Persistent Volume (PV):** Cluster resource representing physical storage
   - **Persistent Volume Claim (PVC):** User's request for storage
   - **StorageClass:** Defines different "classes" of storage with different
     properties

   ```yaml
   # StorageClass
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: fast
   provisioner: kubernetes.io/aws-ebs
   parameters:
     type: gp3

   # PersistentVolumeClaim
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: my-pvc
   spec:
     accessModes:
       - ReadWriteOnce
     storageClassName: fast
     resources:
       requests:
         storage: 100Gi

   # Pod using PVC
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-pod
   spec:
     containers:
       - name: my-container
         image: nginx
         volumeMounts:
         - mountPath: "/data"
           name: my-volume
     volumes:
       - name: my-volume
         persistentVolumeClaim:
           claimName: my-pvc
   ```

10. ## **What is a Helm Chart?**

    _Helm is the **package manager for Kubernetes**, similar to `apt`, `yum`, or
    `brew`._

    **Key Concepts:**

    - **Chart:** A package containing all resource definitions
    - **Release:** An instance of a chart
    - **Repository:** A collection of charts

    **Common Commands:**

    ```bash
    # Add repository
    helm repo add bitnami https://charts.bitnami.com/bitnami

    # Search charts
    helm search repo nginx

    # Install chart
    helm install my-nginx bitnami/nginx

    # List releases
    helm list

    # Upgrade release
    helm upgrade my-nginx bitnami/nginx

    # Rollback
    helm rollback my-nginx 1

    # Uninstall
    helm uninstall my-nginx
    ```

    **Chart Structure:**

    ```
    mychart/
    ├── Chart.yaml
    ├── values.yaml
    ├── charts/
    ├── templates/
    │   ├── deployment.yaml
    │   ├── service.yaml
    │   └── ingress.yaml
    └── templates/NOTES.txt
    ```

11. ## **ConfigMaps and Secrets**

    _ConfigMap - For non-sensitive configuration data_

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: game-config
    data:
      game.properties: |
        enemies=aliens
        lives=3
      ui.properties: |
        color.good=purple
    ```

    **Secret - For sensitive data (base64 encoded):**

    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: mysecret
    type: Opaque
    data:
      username: YWRtaW4=
      password: MWYyZDFlMmU2N2Rm
    ```

    **Using in Pods:**

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: mypod
    spec:
      containers:
        - name: mycontainer
          image: redis
          env:
            - name: SECRET_USERNAME
              valueFrom:
                secretKeyRef:
                  name: mysecret
                  key: username
          volumeMounts:
            - name: config
              mountPath: '/config'
              readOnly: true
      volumes:
        - name: config
          configMap:
            name: game-config
    ```

12. ## **Rolling Updates & Rollbacks**

    **Deployment Strategy:**

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-deployment
    spec:
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxSurge: 25%
          maxUnavailable: 25%
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
            - name: nginx
              image: nginx:1.14.2
              ports:
                - containerPort: 80
    ```

    **Rollout Commands:**

    ```bash
    # Check rollout status
    kubectl rollout status deployment/my-deployment

    # View rollout history
    kubectl rollout history deployment/my-deployment

    # Rollback to previous version
    kubectl rollout undo deployment/my-deployment

    # Rollback to specific revision
    kubectl rollout undo deployment/my-deployment --to-revision=2

    # Pause/resume rollout
    kubectl rollout pause deployment/my-deployment
    kubectl rollout resume deployment/my-deployment
    ```

13. ## **Autoscaling in Kubernetes**

    **Horizontal Pod Autoscaler (HPA):**

    ```yaml
    apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: my-app-hpa
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: my-app
      minReplicas: 2
      maxReplicas: 10
      metrics:
        - type: Resource
          resource:
            name: cpu
            target:
              type: Utilization
              averageUtilization: 50
    ```

    **Vertical Pod Autoscaler (VPA):**

    ```yaml
    apiVersion: autoscaling.k8s.io/v1
    kind: VerticalPodAutoscaler
    metadata:
      name: my-app-vpa
    spec:
      targetRef:
        apiVersion: 'apps/v1'
        kind: Deployment
        name: my-app
      updatePolicy:
        updateMode: 'Auto'
    ```

    **Cluster Autoscaler:**

    - Automatically adjusts the size of the node pool
    - Works with cloud providers (GKE, EKS, AKS)
    - Scales up when pods fail to schedule due to resource constraints
    - Scales down when nodes are underutilized

14. ## **What is a Service Mesh?**

    _A **Service Mesh** provides **observability, security, and traffic
    control** for microservices._

    **Istio Example:**

    ```yaml
    apiVersion: networking.istio.io/v1alpha3
    kind: VirtualService
    metadata:
      name: reviews
    spec:
      hosts:
        - reviews
      http:
        - route:
            - destination:
                host: reviews
                subset: v1
              weight: 90
            - destination:
                host: reviews
                subset: v2
              weight: 10
    ```

    **Benefits:**

    - **Traffic Management:** Routing, circuit breaking
    - **Security:** mTLS, authentication, authorization
    - **Observability:** Metrics, logs, traces
    - **Policy Enforcement:** Rate limiting, quotas

    **Popular Service Meshes:**

    - `Istio`
    - `Linkerd`
    - `Consul Connect`
    - `AWS App Mesh`

15. ## **Debugging Pods**

    **Basic Commands:**

    ```bash
    # Get pod details
    kubectl get pods
    kubectl describe pod <pod-name>

    # View logs
    kubectl logs <pod-name>
    kubectl logs -f <pod-name>  # follow logs
    kubectl logs --previous <pod-name>  # previous container instance

    # Execute commands in pod
    kubectl exec -it <pod-name> -- /bin/sh
    kubectl exec <pod-name> -- env

    # Port forwarding for local access
    kubectl port-forward <pod-name> 8080:80
    ```

    **Advanced Debugging:**

    ```bash
    # Check events in namespace
    kubectl get events --sort-by=.metadata.creationTimestamp

    # Check resource usage
    kubectl top pods
    kubectl top nodes

    # Network debugging
    kubectl run debug-pod --image=nicolaka/netshoot -it --rm

    # Check DNS resolution
    kubectl run dns-test --image=busybox -it --rm -- nslookup kubernetes.default
    ```

    **Common Issues:**

    - `ImagePullBackOff`: Image doesn't exist or credentials wrong
    - `CrashLoopBackOff`: Application crashing on startup
    - `Pending`: Insufficient resources or node issues
    - `ImagePullBackOff`: Registry authentication issues

16. ## **RBAC in Kubernetes**

    **Role + RoleBinding:**

    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      namespace: default
      name: pod-reader
    rules:
    - apiGroups: [""]
      resources: ["pods"]
      verbs: ["get", "watch", "list"]apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: read-pods
      namespace: default
    subjects:
    - kind: User
      name: jane
      apiGroup: rbac.authorization.k8s.io
    roleRef:
      kind: Role
      name: pod-reader
      apiGroup: rbac.authorization.k8s.io
    ```

    **ClusterRole + ClusterRoleBinding:**

    ```yaml
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRole
    metadata:
      name: cluster-admin
    rules:
      - apiGroups: ['*']
        resources: ['*']
        verbs: ['*']
      - nonResourceURLs: ['*']
        verbs: ['*']
    ```

17. ## **Monitoring & Logging**

    **Monitoring (Prometheus + Grafana):**

    ```yaml
    apiVersion: monitoring.coreos.com/v1
    kind: ServiceMonitor
    metadata:
      name: my-app-monitor
    spec:
      selector:
        matchLabels:
          app: my-app
      endpoints:
        - port: web
          interval: 30s
    ```

    - **Logging Stack (EFK):**

      - **Fluentd/Fluent Bit:** Log collection and forwarding
      - **Elasticsearch:** Log storage and indexing
      - **Kibana:** Log visualization and analysis

    - **Alternative: Loki Stack:**

      - **Loki:** Log aggregation system
      - **Promtail:** Log collection agent
      - **Grafana:** Visualization

18. ## **Blue-Green vs Canary Deployments**

    **Blue-Green:**

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: my-app
    spec:
      selector:
        app: my-app
        version: blue # Switch to green later
    ```

    **Canary:**

    ```yaml
    apiVersion: networking.istio.io/v1alpha3
    kind: VirtualService
    metadata:
      name: my-app
    spec:
      hosts:
        - my-app
      http:
        - route:
            - destination:
                host: my-app
                subset: stable
              weight: 90
            - destination:
                host: my-app
                subset: canary
              weight: 10
    ```

19. ## **Securing a Kubernetes Cluster**

    **Best Practices:**

    - **RBAC:** Implement least privilege access
    - **Network Policies:** Restrict pod-to-pod communication
    - **Pod Security Standards:** Use restricted pod security context
    - **Secrets Management:** Use external secret providers (HashiCorp Vault,
      AWS Secrets Manager)
    - **Image Security:** Scan images for vulnerabilities, use trusted
      registries
    - **API Server Security:** Enable audit logging, use network policies
    - **Node Security:** Regular patching, minimize host access
    - **mTLS:** Implement mutual TLS for service-to-service communication

    **Pod Security Example:**

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: security-context-demo
    spec:
      securityContext:
        runAsUser: 1000
        runAsGroup: 3000
        fsGroup: 2000
      containers:
        - name: sec-ctx-demo
          image: busybox
          command: ['sh', '-c', 'sleep 1h']
          securityContext:
            allowPrivilegeEscalation: false
            capabilities:
              drop:
                - ALL
    ```

20. ## **Deployment Strategies - Complete Guide**

    ### 1. Recreate Strategy

    ```yaml
    spec:
      strategy:
        type: Recreate
    ```

    - **Pros:** Simple, ensures all pods run same version
    - **Cons:** Downtime during deployment

    ### 2. Rolling Update (Default)

    ```yaml
    spec:
      strategy:
        type: RollingUpdate
        rollingUpdate:
          maxSurge: 1
          maxUnavailable: 0
    ```

    - **Pros:** Zero downtime, progressive update
    - **Cons:** Multiple versions running simultaneously

    ### 3. Blue-Green Deployment

    - Maintain two identical environments
    - Switch traffic at load balancer level
    - **Pros:** Instant rollback, easy testing
    - **Cons:** Resource intensive (2x resources)

    ### 4. Canary Deployment

    - Release to small percentage of users
    - Gradually increase traffic to new version
    - **Pros:** Risk mitigation, real-user testing
    - **Cons:** Complex setup, requires traffic control

    ### 5. A/B Testing

    - Route users to different versions based on criteria
    - Compare business metrics between versions
    - **Pros:** Data-driven decisions, user segmentation
    - **Cons:** Complex analytics setup

    ### 6. Shadow Deployment

    - Send copy of production traffic to new version
    - No impact on users, test with real load
    - **Pros:** Real-world testing without risk
    - **Cons:** Complex setup, resource intensive

21. ## **Monolith vs Microservices in Kubernetes**

    ### Monolithic Architecture

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: monolith-app
    spec:
      replicas: 3
      template:
        spec:
          containers:
            - name: monolith
              image: mycompany/monolith:latest
              ports:
                - containerPort: 8080
    ```

    ### Microservices Architecture

    ```yaml
    # User Service
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: user-service
    spec:
      replicas: 2
      template:
        spec:
          containers:
          - name: user-service
            image: mycompany/user-service:latest# Order Service
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: order-service
    spec:
      replicas: 3
      template:
        spec:
          containers:
          - name: order-service
            image: mycompany/order-service:latest# Payment Service
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: payment-service
    spec:
      replicas: 2
      template:
        spec:
          containers:
          - name: payment-service
            image: mycompany/payment-service:latest
    ```

    ### Comparison

    | Aspect          | Monolith                | Microservices               |
    | --------------- | ----------------------- | --------------------------- |
    | Development     | Single codebase         | Independent teams           |
    | Deployment      | All or nothing          | Independent deployments     |
    | Scaling         | Scale entire app        | Scale individual services   |
    | Technology      | Homogeneous             | Polyglot (mixed tech stack) |
    | Complexity      | Simple deployment       | Complex orchestration       |
    | Fault Isolation | Single point of failure | Isolated failures           |

22. ## **Kubernetes Operators**

    _Operators are Kubernetes-native applications that extend Kubernetes API to
    manage complex stateful applications._

    **Operator Patterns:**

    - **CRDs (Custom Resource Definitions):** Extend API
    - **Custom Controllers:** Manage app lifecycle
    - **Operator SDK:** Framework to build operators

    ### Example: Database Operator

    ```yaml
    apiVersion: databases.example.com/v1
    kind: Database
    metadata:
      name: my-database
    spec:
      databaseName: myapp
      size: 3
      version: '12'
      backup:
        enabled: true
        schedule: '0 2 * * *'
    ```

23. ## **Kubernetes Resource Management**

    ### Resource Requests and Limits

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: frontend
    spec:
      containers:
        - name: app
          image: myapp:latest
          resources:
            requests:
              memory: '64Mi'
              cpu: '250m'
            limits:
              memory: '128Mi'
              cpu: '500m'
        - name: log-aggregator
          image: log-aggregator:latest
          resources:
            requests:
              memory: '64Mi'
              cpu: '250m'
            limits:
              memory: '128Mi'
              cpu: '500m'
    ```

    ### Quality of Service (QoS) Classes

    - **Guaranteed:** All containers have limits = requests
    - **Burstable:** At least one container has request < limit
    - **BestEffort:** No requests or limits specified

24. ## **Kubernetes Namespaces**

    ### Namespace Management

    ```bash
    # Create namespace
    kubectl create namespace production

    # Apply resources in namespace
    kubectl apply -f manifest.yaml -n production

    # View across namespaces
    kubectl get pods --all-namespaces
    ```

    ### Resource Quotas

    ```yaml
    apiVersion: v1
    kind: ResourceQuota
    metadata:
      name: compute-resources
      namespace: production
    spec:
      hard:
        requests.cpu: '2'
        requests.memory: 4Gi
        limits.cpu: '4'
        limits.memory: 8Gi
        pods: '10'
    ```

25. ## **Troubleshooting Common Issues**

    - **Pod Stuck in Pending**

    ```bash
    kubectl describe pod <pod-name>
    kubectl get events --sort-by=.metadata.creationTimestamp
    ```

    - **Image Pull Errors**

    ```bash
    kubectl describe pod <pod-name>
    ```

    - **CrashLoopBackOff**

    ```bash
    kubectl logs <pod-name> --previous
    kubectl describe pod <pod-name>
    ```

    - **Service Not Working**

    ```bash
    kubectl get endpoints <service-name>
    kubectl run test --image=busybox -it --rm -- nslookup <service-name>
    ```

    - **Persistent Volume Issues**

    ```bash
    kubectl get pv,pvc
    kubectl describe pvc <pvc-name>
    ```

26. ## **Kubernetes Best Practices**

    ### Application Design

    - Use declarative configs (YAML)
    - Implement liveness/readiness probes
    - Use resource requests & limits
    - Prefer stateless apps

    ### Security

    - Implement RBAC (least privilege)
    - Run containers as non-root
    - Regularly update images & K8s
    - Scan images for vulnerabilities

    ### Operations

    - Use namespaces for isolation
    - Apply resource quotas
    - Set up monitoring & alerting
    - Use Helm/Kustomize for packaging
    - Plan backup & disaster recovery

    ### Networking

    - Apply Network Policies
    - Use Ingress for traffic
    - Enable service discovery
    - Adopt Service Mesh for complex microservices
