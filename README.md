I am going to make Documentation for all pricatals and home labs as much I can + Diagrams

linux arch + certificaion in linux 
- Boot process
- File sytem
- Permissions
- Systemd
- Package managters
- Debugging skills
- Finding /reading logs
- Networking Fundamentals
- Bash scripting -- every thing of pipeline can be replaced by BashScripting

Vim text editor Commands
   i, I
         change to insert mode
h, j, k, l
            move left, down, up, right
w, b, e, ge
            move word at a time
[n][action/movement]
            do n times, e.g. 3w
x, X
            remove a character
a, A
            append
f[char]
            move to next given char in line
F[char]
            move to previous char in line
; and ,
            repeat last f or F
/yourtext and then: n, N
            Search text
d[movement]
            delete by giving movement
r[char]
            replaces character below cursor
0, $
            move to start/end of line
o, O
            add new line
%
            Goto corresponding parentheses
ci[movement]
            change inside of given movement
D
            delete to end of line
S
            clear current line; to insert mode
gg / G
            move to start / end of buffer
yy
            copy current line
p
            Paste copied text after cursor
  
-- Certification -- RHCSA  or LIPIC-1

Containers
- Docker
- DockerFile
- Container sercuriy
- Running multiple containers
- Docker Networking
- Dev Containers

Programing Language
- Mainly for connecting tools & API'S
- Learn the Fundamentals
    * Varibales
    * Functions
    * OOP
    * Labraries

Git

Learn to love Yaml 
Yaml is used for:
    * ansible
    * Kubernetes
    * github Actions
    * Azure DevOps pipelines

Python and Go Language
 * Most poplular language in AI and MLOps 

 https://www.exersism.org/tracks/python/consepts
http://www.freecodecamp.org
100 days of python on udemy
* use code to automate small thinsg for yourself
* www.freepublicapis.com
book - learn to automate boaring stuff

Cloud 
 - AWS-associate 100 jobs on it
    * Adrian Contrill 
    * Kodekloud
    * Aws Skill Builders
    *
 - AZ - 104 Azure administrator 50 jobs on it
   * Micsofoft Learn
   * John Savill youtube 

 - GCP 
   * Has smaller market space
   * https://cloud.google.com/learn/training

Infrastructure as Code IaC
  * Bisep for Microsoft
  * Terraform

Ansible 
  
Cloud elements
 * Databases
 * Storage and Backup
 * Networking / azur 104 course has networing deep tutorial
 * IAM / Entra ID

CI/CD
* Jenkins
* ArgoCD
* Githup Action
* GitLab

Kubernetes
* https://youtube.com/clip/UgkxGHiVqCiH5idb0J-tTlwvrKGS63ywQ5fQ?si=tn8GSlxT04UvbDmG
 * Certification - CKA,CKAD,CKS
 * kubectl set image deployment/nginx-deployment -n nginx  nginx=nginx:latest
1. Cluster Creation / Startup Errors

Errors:

Failed to pull image

Node NotReady

CrashLoopBackOff for control plane pods

kubelet not running or apiserver not reachable

Troubleshooting:

Check infrastructure (VM status, disk, CPU, memory).

Verify network connectivity between nodes.

Check systemctl status kubelet and logs (journalctl -xeu kubelet).

Inspect docker/containerd logs to see why control plane containers failed.

Ensure correct certificates & tokens are used for joining nodes.

🔹 2. Node Errors

Errors:

kubectl get nodes shows NotReady

Node stuck in SchedulingDisabled

Kubelet has insufficient memory/disk

Troubleshooting:

Run kubectl describe node <node-name> to check conditions.

Verify kubelet logs: journalctl -u kubelet.

Check node resource usage (top, df -h).

Confirm CNI (network plugin) is installed correctly.

Drain & restart node if corrupted:

kubectl drain <node> --ignore-daemonsets --delete-emptydir-data

🔹 3. Pod Scheduling Errors

Errors:

Pending pods

0/3 nodes are available: Insufficient CPU

Taints prevent scheduling

Troubleshooting:

kubectl describe pod <pod-name> → look at "Events" section.

Check resource requests vs. node capacity.

Verify tolerations and nodeSelector/affinity rules.

Remove taints if unintentional:

kubectl taint nodes <node> key=value:NoSchedule-

🔹 4. Pod Runtime Errors

Errors:

CrashLoopBackOff

ImagePullBackOff

OOMKilled

Completed but app not working

Troubleshooting:

Check logs:

kubectl logs <pod> -n <namespace>


If multiple containers:

kubectl logs <pod> -c <container-name>


Check events:

kubectl describe pod <pod>


Common causes:

Wrong image name / private registry auth

App crashes due to config/env/secret issues

Resource limits too low

🔹 5. Service & Networking Errors

Errors:

Pod-to-pod communication fails

Service ClusterIP not reachable

External LoadBalancer not working

DNS resolution failure inside cluster

Troubleshooting:

Verify CNI plugin:

kubectl get pods -n kube-system


Check CoreDNS logs:

kubectl logs -n kube-system -l k8s-app=kube-dns


Test DNS resolution inside pod:

kubectl exec -it <pod> -- nslookup kubernetes.default


Confirm iptables rules aren’t blocked.

For LoadBalancer: check cloud provider integration.

🔹 6. Storage Errors

Errors:

Pod stuck in ContainerCreating with PVC pending

Unable to attach or mount volumes

Error from CSI driver

Troubleshooting:

Check PVC & PV status:

kubectl get pvc,pv


Describe PVC for error messages.

Ensure storage class exists:

kubectl get storageclass


Check CSI plugin logs (kubectl logs -n kube-system <csi-pod>).

🔹 7. API Server / Control Plane Errors

Errors:

kubectl get ... hangs

etcdserver: request timed out

apiserver connection refused

Troubleshooting:

Check API server logs:

journalctl -u kube-apiserver


Verify etcd cluster health:

ETCDCTL_API=3 etcdctl endpoint health --endpoints <list>


Look for certificate expiry issues.

Ensure control plane nodes can reach each other.

🔹 8. RBAC & Authentication Errors

Errors:

User "xyz" cannot list resource ...

Forbidden: service account not allowed

Troubleshooting:

Check Role/ClusterRole + RoleBinding/ClusterRoleBinding.

Inspect service account tokens.

Use kubectl auth can-i to test permissions:

kubectl auth can-i get pods --as=system:serviceaccount:default:my-sa

🔹 9. Performance & Scaling Issues

Errors:

High pod restart count

Slow API response

Cluster autoscaler not scaling

Troubleshooting:

Monitor resource usage with Prometheus/Grafana.

Check HPA:

kubectl get hpa


Inspect cluster autoscaler logs.

Verify node pool scaling policies in cloud provider.

✅ General Debugging Commands:

kubectl get events --sort-by=.metadata.creationTimestamp

kubectl describe <resource>

kubectl logs

kubectl top nodes

kubectl top pods

journalctl -u kubelet

kubectl get componentstatuses (deprecated, but useful)

Artificial Intelligent
* Book Artifical intellingence A Guide for Thingking Humans by Melanie Mitchell
