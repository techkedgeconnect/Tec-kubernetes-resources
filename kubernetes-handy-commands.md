# Kubernetes Troubleshooting Command
Given that Kubernetes is a dynamic and distributed system, issues can stem from multiple areas, including application misconfigurations, networking problems, resource limitations, or node failures. Debugging and diagnosing issues in a Kubernetes cluster involves identifying and resolving problems with various cluster resources, such as pods, services, nodes, and deployments. 

When troubleshooting, it’s crucial to pinpoint the source of the problem, whether it’s a pod crashing, an unreachable service, or malfunctioning nodes. 

# Common issues include:
  - Pods stuck in the Pending or CrashLoopBackOff states
  - Services not routing traffic correctly
  - Resource exhaustion on nodes (CPU/memory)
  - Network policies or DNS resolution failures
    
# Why These Commands are Handy
The following kubectl commands provide direct insights into the cluster's status and resources, helping you to:

Monitor Resource Health
- Commands like kubectl get pods, kubectl describe, and kubectl top help track pod status, CPU, and memory usage to identify resource bottlenecks or failures.
  
Gather Logs and Events
- Commands like kubectl logs and kubectl get events offer visibility into pod logs and cluster events, useful for analyzing application errors and cluster activities.

Interact with Pods
- kubectl exec allows running commands inside a pod for debugging, while kubectl port-forward lets you access applications running in pods.

Network and DNS Troubleshooting
- Commands such as kubectl exec with DNS tools (nslookup, dig) are used to check connectivity between services, helping diagnose network issues.
  
Handling Deployments
- kubectl rollout status and kubectl rollout undo are key for tracking and reverting failed deployments, ensuring smooth application updates.

These commands offer a structured approach to diagnosing and resolving issues, allowing you to quickly find the root cause of problems and restore the cluster to a healthy state.

1. kubectl logs command
   - It fetches the logs of a running pod (or specific container). It is one of the most common ways to troubleshoot issues with applications running in containers.
   Usage
   - It is used to analyze errors, stack traces, or application behavior by inspecting logs directly from the pod.
     - kubectl logs <pod_name>
     - kubectl logs <pod_name> -c <container_name>  # For multi-container pods
     - kubectl logs -f <pod_name>  # Follow log output
    
2. Describe a Resource
   - This comamnd provides detailed information about a resource, including events, conditions, and any errors encountered during scheduling, deployment, or runtime.
   Usage
   - It is useful for diagnosing pod creation failures, service issues, or deployment progress by checking events and status updates.
     - kubectl describe pod <pod_name>
     - kubectl describe service <svc_name>
     - kubectl describe deployment <deployment_name>

3. Check Pod Status
   - This command lists pods with detailed status (Running, Pending, Failed) and other information like node assignment and IP addresses.
   Usage
   - This command help to get a quick overview of all pods in a namespace or across namespaces. The wide output also includes node names and other critical information.
     - kubectl get pods -o wide
     - kubectl get pods --all-namespaces

4. Get Cluster Events
   - This command lists events across the cluster. Events include resource creation, updates, scaling, and errors.
   Usage
   - Events are a great way to troubleshoot why a pod, deployment, or service isn’t functioning properly, particularly during startup or scaling issues.
     - kubectl get events

5. Exec into a Pod
   - Executes a command inside a running container, or opens an interactive terminal (-it) to debug the environment of the container.
   Usage
   - It is use to run troubleshooting commands (e.g., checking file paths, environment variables, DNS resolution) or to debug a malfunctioning pod from the inside.
     - kubectl exec -it <pod_name> -- /bin/bash
     - kubectl exec -it <pod_name> -- <command>

6. Port Forward to a Pod
   - It is used to forward a local port to a pod’s port, allowing you to access the service running inside the pod locally without exposing it externally.
   Usage
   - It is useful for debugging services that are running inside pods when there is no external service or ingress setup.
     - kubectl port-forward <pod_name> <local_port>:<pod_port>

7. Check Resource Usage (Top Command)
   - You can use this command to show resource consumption for pods and nodes (CPU and memory usage).
   Usage
   - It helps to identify resource bottlenecks or overconsumption, which may lead to performance issues or crashes.
     - kubectl top pod
     - kubectl top node


Here’s a comprehensive list of Kubernetes troubleshooting commands, their explanations, and usage, which are essential for resolving issues in a Kubernetes cluster.

1. View Pod Logs
Command:

bash
Copy code
kubectl logs <pod_name>
kubectl logs <pod_name> -c <container_name>  # For specific container in a multi-container pod
kubectl logs -f <pod_name>  # Follow log output
Explanation:
Fetches the logs of a running pod (or specific container). This is one of the most common ways to troubleshoot issues with applications running in containers.

Usage:
To analyze errors, stack traces, or application behavior by inspecting logs directly from the pod.

2. Describe a Resource
Command:

bash
Copy code
kubectl describe pod <pod_name>
kubectl describe service <svc_name>
kubectl describe deployment <deployment_name>
Explanation:
Provides detailed information about a resource, including events, conditions, and any errors encountered during scheduling, deployment, or runtime.

Usage:
Useful for diagnosing pod creation failures, service issues, or deployment progress by checking events and status updates.

3. Check Pod Status
Command:

bash
Copy code
kubectl get pods -o wide
kubectl get pods --all-namespaces
Explanation:
Lists pods with detailed status (Running, Pending, Failed) and other information like node assignment and IP addresses.

Usage:
To get a quick overview of all pods in a namespace or across namespaces. The wide output also includes node names and other critical information.

4. Get Cluster Events
Command:

bash
Copy code
kubectl get events
Explanation:
Lists events across the cluster. Events include resource creation, updates, scaling, and errors.

Usage:
Events are a great way to troubleshoot why a pod, deployment, or service isn’t functioning properly, particularly during startup or scaling issues.

5. Exec into a Pod
Command:

bash
Copy code
kubectl exec -it <pod_name> -- /bin/bash
kubectl exec -it <pod_name> -- <command>
Explanation:
Executes a command inside a running container, or opens an interactive terminal (-it) to debug the environment of the container.

Usage:
Use this to run troubleshooting commands (e.g., checking file paths, environment variables, DNS resolution) or to debug a malfunctioning pod from the inside.

6. Port Forward to a Pod
Command:

bash
Copy code
kubectl port-forward <pod_name> <local_port>:<pod_port>
Explanation:
Forwards a local port to a pod’s port, allowing you to access the service running inside the pod locally without exposing it externally.

Usage:
Useful for debugging services that are running inside pods when there is no external service or ingress setup.

7. Check Resource Usage (Top Command)
Command:

bash
Copy code
kubectl top pod
kubectl top node
Explanation:
Shows resource consumption for pods and nodes (CPU and memory usage).

Usage:
Helps to identify resource bottlenecks or overconsumption, which may lead to performance issues or crashes.

8. View Persistent Volume (PV) and Persistent Volume Claims (PVC)
   - It is used to list all Persistent Volumes and Persistent Volume Claims, along with their statuses and details.
   Usage
   - Used to troubleshoot storage-related issues such as volume binding, access modes, or storage capacity.
     - kubectl get pv
     - kubectl get pvc
     - kubectl describe pvc <pvc_name>

9. Check Pod Restarts
   - It shows pods that have failed, completed, or have restart counts (useful to detect crash loops).
   Usage
   - It is useful for identifying and debugging crash loops (e.g., CrashLoopBackOff) or pods that are stuck in Pending or Failed states.
     - kubectl get pods --field-selector=status.phase!=Running
     - kubectl get pods --all-namespaces --field-selector=status.phase=Failed

10. Inspecting Pod Readiness and Liveness Probes
    - In the pod description, you can inspect readiness and liveness probes to determine why a pod may not be marked as "Ready" or is getting killed by the Kubernetes scheduler.
    Usage
    - This command is used to troubleshoot issues with probes (e.g., when the pod is constantly restarting due to failing liveness checks).
      - kubectl describe pod <pod_name>

11. Checking for Failed Jobs
    - This command lists all jobs and their statuses. Describing jobs can reveal the reason for failure or stuck jobs.
    Usage
    - It is useful for understanding why scheduled jobs (e.g., cron jobs) failed or didn’t complete successfully.
      - kubectl get jobs
      - kubectl describe job <job_name>
      - kubectl get pods --field-selector=status.phase=Failed

12. Checking Pod DNS Resolution
    - This command tests DNS resolution from inside the pod.
    Usage
    - It is helpful in troubleshooting service-to-service communication issues when DNS resolution is suspected to be the problem.
      - kubectl exec -it <pod_name> -- nslookup <service_name>
      - kubectl exec -it <pod_name> -- dig <service_name>

13. Identify Unused or Orphaned Resources
    - Lists replica sets, services, and other resources that may be orphaned or not in use.
    Usage
    - It is useful for identifying unused resources that can be cleaned up to free cluster resources.
      - kubectl get rs
      - kubectl get svc

14. Investigate CrashLoopBackOff
    - The CrashLoopBackOff occurs when a pod is stuck in a crash loop due to some error during startup. The logs and the detailed description of the pod can reveal the cause.
    Usage
    - It is helpful for determining the root cause of a pod’s failure (e.g., misconfiguration, resource limits, application errors).
      - kubectl describe pod <pod_name>
      - kubectl logs <pod_name>
      - kubectl get pod <pod_name> -o jsonpath='{.status.containerStatuses[0].state.waiting.message}'

15. Debug StatefulSets
    - This command describes StatefulSets and lists the associated pods, which often run stateful applications (like databases).
    Usage
    - It is useful for troubleshooting issues with stateful applications where maintaining stable network identities and storage is critical.
      - kubectl describe statefulset <statefulset_name>
      - kubectl get pods -l app=<statefulset_name>

16. Get Deployment Rollout Status
    - This command shows the rollout status of a deployment, including progress, failed updates, or reasons for rollback.
    Usage
    - It is used to check if a new version of an application has been successfully deployed, and to monitor ongoing rollouts.
      - kubectl rollout status deployment <deployment_name>

17. Rollback a Failed Deployment
    - This command help to roll back a failed or problematic deployment to the previous stable version.
    Usage
    - This is useful when a new deployment introduces bugs or issues, and you need to quickly restore a working version.
      - kubectl rollout undo deployment <deployment_name>

18. Checking for Resource Quotas and Limits
    - This ncommand help to list and describes resource quotas and limits set for a namespace or cluster.
    Usage
    - It is used to troubleshoot resource allocation issues, such as when pods are pending because they exceed set quotas or limits.
      - kubectl get resourcequotas
      - kubectl describe resourcequota <quota_name>
      - kubectl get limits

19. Network Debugging (Network Policies)
    - This command lists and describes network policies that restrict or allow network traffic between pods.
   Usage
   - It is used to troubleshoot network connectivity issues caused by overly restrictive network policies between services.

20. Dry Run to Preview Changes
    - This command help to simulate the creation or update of resources without applying any actual changes.
    Usage
    - It is useful for verifying if a configuration is correct before applying it to the cluster, thus reducing the risk of unintended changes.
      - kubectl apply -f <file.yaml> --dry-run=client

21. Diagnose Node Issues 
    - This command shows detailed node information, such as the number of pods scheduled, resource capacity, and any issues or taints on the node.
    Usage
    - It is used to troubleshoot node-related issues like resource exhaustion, taints, or node failure.
      - kubectl describe node <node_name>
      - kubectl get nodes -o wide
      - kubectl get pods --all-namespaces --field-selector spec.nodeName=<node_name>
