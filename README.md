I am going to make Documentation for all pricatals and home labs as much I can + Diagrams

linux arch + certificaion in linux

Boot process
File sytem
Permissions
Systemd
Package managters
Debugging skills
Finding /reading logs
Networking Fundamentals
Bash scripting – every thing of pipeline can be replaced by BashScripting
Vim text editor Commands
---------- i, I
-change to insert mode
h, j, k, l
* move left, down, up, right
w, b, e, ge
*move word at a time
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

scp command 
            rsync -avz -e "ssh -i /path/to/private_key.pem" /local/dir/ user@remote_host:/remote/dir/

| Option                | Description                                                            |
| --------------------- | ---------------------------------------------------------------------- |
| `-a`                  | Archive mode (preserves permissions, symbolic links, timestamps, etc.) |
| `-v`                  | Verbose (shows progress)                                               |
| `-z`                  | Compress data during transfer                                          |
| `-h`                  | Human-readable numbers (for file sizes, etc.)                          |
| `--progress`          | Show progress during transfer                                          |
| `--delete`            | Delete files in destination that don’t exist in source                 |
| `-e "ssh"`            | Use SSH as the transport mechanism                                     |
| `--exclude='pattern'` | Exclude files or directories matching the pattern                      |
| `--dry-run`           | Show what would be done without making changes                         |


            Safe Two-Way Sync with Tools Built on rsync
To handle conflicts and timestamps safely, you can use wrappers around rsync, such as:
🧠 Option 1: unison
Cross-platform (Linux, macOS, Windows)
Tracks changes on both sides
Handles conflicts interactively
Example:
unison /local ssh://user@remote//remote

✅ Truly synchronizes both directions safely

| Part                            | Meaning                                                |
| ------------------------------- | ------------------------------------------------------ |
| `-a`                            | Archive mode (preserves permissions, timestamps, etc.) |
| `-v`                            | Verbose                                                |
| `-z`                            | Compress during transfer                               |
| `-e "ssh -i key.pem"`           | Use SSH with a specific private key                    |
| `/local/dir/`                   | Source directory                                       |
| `user@remote_host:/remote/dir/` | Destination path on remote system                      |

Perfect 👍 Here’s an improved and well-structured **README.md** draft for your “Linux Networking Commands” section — first a list, then detailed explanations for each:

````markdown
# **Networking in Linux**

Linux provides many powerful tools to view, test, and manage network configurations and connections.  
Below is a list of commonly used networking commands.

---

## **📋 Command List**

| Command | Description |
|----------|--------------|
| `ifconfig` | Display or configure network interfaces |
| `ip` | Manage IP addresses, routes, and interfaces (modern replacement for ifconfig) |
| `netstat` | Display network connections, routing tables, and interface statistics |
| `ss` | Display detailed socket statistics (replacement for netstat) |
| `ping` | Test network connectivity to another host |
| `traceroute` | Show the route packets take to a destination |
| `nslookup` | Query DNS records for a domain |
| `dig` | Advanced DNS lookup utility |
| `route` | View or manipulate the IP routing table |
| `hostname` | Show or set the system’s hostname |
| `curl` | Transfer data from or to a server |
| `wget` | Download files from the web using HTTP, HTTPS, or FTP |
| `ethtool` | Display or modify Ethernet device parameters |
| `tcpdump` | Capture and analyze network packets |
| `nmap` | Network exploration and security auditing tool |

---

## **🧩 Command Explanations**

### **1. ifconfig**
Used to configure and display network interface information.

```bash
ifconfig -a          # Show all interfaces
sudo ifconfig eth0 up    # Enable interface
sudo ifconfig eth0 192.168.1.10 netmask 255.255.255.0
````

> ⚠️ Deprecated on modern systems — use `ip` instead.

---

### **2. ip**

Modern replacement for `ifconfig`, providing detailed control over networking.

```bash
ip addr show           # Show IP addresses
ip link set eth0 up    # Bring interface up
ip route show          # Display routing table
```

---

### **3. netstat**

Displays active network connections, ports, and routing tables.

```bash
netstat -a       # Show all connections
netstat -tulpn   # Show listening ports with process names
```

> ⚠️ Replaced by `ss` in newer systems.

---

### **4. ss**

Socket statistics — faster, more detailed replacement for `netstat`.

```bash
ss -tulpn     # Show listening TCP/UDP ports
ss -s         # Show summary of socket usage
```

---

### **5. ping**

Used to test network connectivity to another host.

```bash
ping google.com
ping -c 4 8.8.8.8
```

---

### **6. traceroute**

Traces the path packets take to reach a destination.

```bash
traceroute google.com
traceroute -I 8.8.8.8
```

---

### **7. nslookup**

Queries DNS records for a domain.

```bash
nslookup example.com
```

---

### **8. dig**

Advanced DNS query tool with detailed output.

```bash
dig example.com
dig +short example.com
```

---

### **9. route**

Displays or modifies the system’s routing table.

```bash
route -n
sudo route add default gw 192.168.1.1
```

---

### **10. hostname**

Displays or sets the system hostname.

```bash
hostname
sudo hostnamectl set-hostname myserver
```

---

### **11. curl**

Transfers data to/from a server using URLs (HTTP, FTP, etc).

```bash
curl https://example.com
curl -I https://example.com   # Fetch only headers
```

---

### **12. wget**

Downloads files from the web via command line.

```bash
wget https://example.com/file.zip
```

---

### **13. ethtool**

Displays Ethernet interface settings and statistics.

```bash
ethtool eth0
```

---

### **14. tcpdump**

Captures and analyzes network traffic.

```bash
sudo tcpdump -i eth0
sudo tcpdump -i eth0 port 80
```

---

### **15. nmap**

Scans networks and identifies hosts, open ports, and services.

```bash
nmap 192.168.1.0/24
nmap -sS -p 22,80 192.168.1.10
```

---

## **✅ Summary**

| Category              | Commands                    |
| --------------------- | --------------------------- |
| Interface Management  | `ifconfig`, `ip`, `ethtool` |
| Connection Monitoring | `netstat`, `ss`, `tcpdump`  |
| Network Testing       | `ping`, `traceroute`        |
| DNS Tools             | `nslookup`, `dig`           |
| Routing               | `route`                     |
| Web Utilities         | `curl`, `wget`              |
| Security/Scanning     | `nmap`                      |

---

## **📘 Next Steps**

* Learn how to combine these tools in shell scripts.
* Practice troubleshooting real network issues.
* Explore advanced tools like `wireshark`, `iptables`, and `firewalld`.

```

Would you like me to add **practical scenarios** next (like “Check why a server is unreachable” or “Find which process is using a port”)? That would make this README even more hands-on.
```


 
– Certification – RHCSA or LIPIC-1

Containers

Docker
DockerFile
Container sercuriy
Running multiple containers
Docker Networking
Dev Containers
Programing Language

Mainly for connecting tools & API’S
Learn the Fundamentals
Varibales
Functions
OOP
Labraries
Git

Learn to love Yaml
Yaml is used for:
* ansible
* Kubernetes
* github Actions
* Azure DevOps pipelines

Python and Go Language

Most poplular language in AI and MLOps
https://www.exersism.org/tracks/python/consepts
http://www.freecodecamp.org
100 days of python on udemy

use code to automate small thinsg for yourself
www.freepublicapis.com
book - learn to automate boaring stuff
Cloud

AWS-associate 100 jobs on it

Adrian Contrill
Kodekloud
Aws Skill Builders
AZ - 104 Azure administrator 50 jobs on it

Micsofoft Learn
John Savill youtube
GCP

Has smaller market space
https://cloud.google.com/learn/training
Infrastructure as Code IaC

Bisep for Microsoft
Terraform
Ansible

Cloud elements

Databases
Storage and Backup
Networking / azur 104 course has networing deep tutorial
IAM / Entra ID
CI/CD

Jenkins
ArgoCD
Githup Action
GitLab
Kubernetes

https://youtube.com/clip/UgkxGHiVqCiH5idb0J-tTlwvrKGS63ywQ5fQ?si=tn8GSlxT04UvbDmG
Certification - CKA,CKAD,CKS
kubectl set image deployment/nginx-deployment -n nginx nginx=nginx:latest
Cluster Creation / Startup Errors
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

kubectl describe pod <pod-name> → look at “Events” section.

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

kubectl exec -it <pod> – nslookup kubernetes.default

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

kubectl get … hangs

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

User “xyz” cannot list resource …

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

Book Artifical intellingence A Guide for Thingking Humans by Melanie Mitchell
