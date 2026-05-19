# DevOps Engineer Interview Quick Revision Notes (2 Years Experience)

---

# 1. Linux & Windows Administration

## Common Linux Commands

```bash
top
htop
df -h
free -m
du -sh *
ss -tulpn
ps aux
grep
awk
sed
journalctl -u nginx
systemctl status nginx
tail -f /var/log/messages
chmod
chown
scp
rsync
crontab -e
```

## Important Linux Concepts
- Process management
- File permissions
- SSH troubleshooting
- Package managers (apt/yum)
- Service management with systemd

## Windows Basics
- IIS
- RDP
- Event Viewer
- PowerShell
- Windows Services

---

# 2. Networking & Security

## TCP/IP Basics
- TCP = reliable communication
- UDP = faster but no guarantee
- IP = addressing system
- DNS = domain to IP conversion

## Common Ports

| Service | Port |
|---|---|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |
| FTP | 21 |
| MySQL | 3306 |
| PostgreSQL | 5432 |
| Jenkins | 8080 |
| Kubernetes API | 6443 |

---

# Security Concepts

## Security Group
- Instance-level firewall
- Stateful

## NACL
- Subnet-level firewall
- Stateless

## NSG
- Azure Network Security Group

## WAF
Protects against:
- SQL Injection
- XSS
- Layer 7 attacks

## VPN
Secure encrypted communication tunnel.

---

# 3. Nginx & Apache

## Nginx Uses
- Reverse Proxy
- Load Balancer
- SSL Termination
- Static File Hosting

## Reverse Proxy Example

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:3000;
    }
}
```

## Useful Commands

```bash
nginx -t
systemctl restart nginx
```

---

# 4. Deployment Strategies

## Rolling Deployment
Update pods gradually without downtime.

## Blue-Green Deployment
Two environments:
- Blue = old
- Green = new

Switch traffic after testing.

## Canary Deployment
Release to small percentage of users first.

## Rollback Strategy
- Keep previous image/version
- Maintain DB backup
- Use version tags

---

# 5. CI/CD Pipeline

## Flow

```text
Code → Build → Test → Scan → Deploy
```

## Jenkins Pipeline Example

```groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t app .'
      }
    }
  }
}
```

## GitLab CI/CD File

```yaml
.gitlab-ci.yml
```

---

# 6. Docker

## Docker vs VM

| Docker | VM |
|---|---|
| Lightweight | Heavy |
| Shares kernel | Separate OS |
| Fast startup | Slow startup |

## Important Commands

```bash
docker ps
docker images
docker build
docker run
docker logs
docker exec -it
docker inspect
docker-compose up
```

## Dockerfile Example

```dockerfile
FROM nginx
COPY . /usr/share/nginx/html
```

---

# 7. Kubernetes

## Core Components

| Component | Purpose |
|---|---|
| Pod | Smallest deployable unit |
| Deployment | Manages replicas |
| Service | Exposes application |
| Ingress | HTTP routing |
| ConfigMap | Non-sensitive configs |
| Secret | Sensitive data |

## Important Commands

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- bash
kubectl apply -f file.yaml
kubectl get svc
kubectl get ingress
```

---

# 8. Monitoring & Logging

## Tools
- Prometheus
- Grafana
- Zabbix
- Site24x7

## Metrics to Monitor
- CPU
- Memory
- Disk
- Network
- Pod Restarts
- Application Errors
- Response Time

---

# 9. Terraform

## Workflow

```bash
terraform init
terraform plan
terraform apply
terraform destroy
```

## Terraform State File
`terraform.tfstate`

Stores infrastructure metadata and current resource mappings.

---

# 10. Ansible

## Inventory File

```ini
[web]
server1
server2
```

## Playbook Example

```yaml
- hosts: web
  tasks:
    - name: install nginx
      apt:
        name: nginx
        state: present
```

## Ad-hoc Command

```bash
ansible all -m ping
```

---

# 11. Git & Branching

## Common Commands

```bash
git clone
git pull
git push
git checkout
git branch
git merge
git rebase
```

## Branching Strategy
- main/master = production
- develop = testing
- feature branches

---

# 12. Cloud Concepts (AWS)

| Service | Purpose |
|---|---|
| EC2 | Virtual Machine |
| S3 | Storage |
| IAM | Access Management |
| RDS | Managed Database |
| VPC | Networking |
| ALB | Load Balancer |
| Route53 | DNS |
| CloudWatch | Monitoring |

---

# 13. Troubleshooting Scenarios

## App Down Checklist

1. Server reachable?
2. CPU/RAM usage?
3. Service running?
4. Check logs
5. DB connectivity
6. Firewall/network issue?
7. Recent deployment changes?

---

# 14. Important Interview Questions & Answers

## How do you deploy applications with zero downtime?

I use rolling deployments or blue-green deployments. In rolling deployment, new instances/pods are updated gradually while old ones still serve traffic. Health checks and load balancers ensure users only hit healthy instances. If something fails, rollback is performed immediately.

---

## Difference between Security Group and NACL

| Security Group | NACL |
|---|---|
| Instance level | Subnet level |
| Stateful | Stateless |
| Allow rules only | Allow + Deny rules |
| Automatically allows return traffic | Return traffic must be explicitly allowed |

---

## Difference between Docker and Kubernetes

| Docker | Kubernetes |
|---|---|
| Container platform | Container orchestration platform |
| Runs containers | Manages containers at scale |
| Single host focus | Multi-node cluster management |
| Packaging app | Auto-scaling and orchestration |

---

## What happens when you type google.com in browser?

1. Browser checks cache.
2. DNS resolves domain to IP.
3. TCP handshake occurs.
4. HTTPS connection established.
5. Request reaches server/load balancer.
6. Server sends response.
7. Browser renders webpage.

---

## How does DNS work?

DNS converts domain names into IP addresses. Request flows through browser cache → OS cache → DNS resolver → root server → TLD server → authoritative DNS server.

---

## Explain Reverse Proxy

A reverse proxy sits between users and backend servers. It forwards client requests to backend applications and provides SSL termination, security, caching, and load balancing.

---

## Explain Rolling Deployment

Rolling deployment updates application instances gradually instead of shutting down all at once, ensuring zero downtime.

---

## How do you troubleshoot pod failures?

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

Check:
- Image issues
- Resource limits
- ConfigMap/Secret issues
- Node status
- Network connectivity

---

## How do you secure production infrastructure?

- Least privilege IAM access
- Security Groups/firewalls
- HTTPS & SSL
- Secure secret management
- Regular patching
- Monitoring and logging
- VPN/private subnets
- Restricted SSH access
- Backups & DR strategy

---

## Explain Terraform State File

Terraform state file stores infrastructure metadata and tracks resource states to detect infrastructure changes during plan/apply operations.

---

## Difference between ConfigMap and Secret

| ConfigMap | Secret |
|---|---|
| Non-sensitive data | Sensitive data |
| Plain configs | Encoded/encrypted values |
| App configs | Passwords/API keys |

---

## How do you monitor production systems?

I use Prometheus for metrics collection, Grafana for dashboards, and alerting systems for proactive issue detection. I monitor CPU, memory, disk, logs, uptime, response time, and pod health.

---

## Explain Load Balancing

Load balancer distributes incoming traffic across multiple servers or pods to improve availability, scalability, and fault tolerance.

---

## How do you rollback deployments?

### Kubernetes Rollback

```bash
kubectl rollout undo deployment <deployment-name>
```

### CI/CD Rollback
Deploy previous stable image/tag and restore backups if needed.

---

# 15. Kubernetes Troubleshooting Commands

## Check Listening Ports

```bash
ss -tulpn
```

## Check Specific Port

```bash
ss -tulpn | grep 8080
```

## Check Service Status

```bash
systemctl status nginx
```

## Check Logs

```bash
journalctl -u nginx
```

---

# 16. Tell Me About Yourself (Sample)

> I have around 2 years of experience in DevOps and cloud infrastructure. I’ve worked on CI/CD pipelines using Jenkins and GitLab CI, containerized deployments with Docker and Kubernetes, infrastructure automation using Terraform and Ansible, and monitoring using Prometheus and Grafana. I also handle Linux administration, troubleshooting production issues, and AWS cloud infrastructure management.

---

# 17. Final Quick Keywords

- High Availability
- Scalability
- Automation
- Infrastructure as Code
- Reverse Proxy
- Load Balancing
- Observability
- Auto Scaling
- Zero Downtime
- Failover
- Immutable Infrastructure

---

# 18. Interview Tips

- Explain with real examples
- Focus on troubleshooting steps
- Speak clearly and confidently
- Mention production experience
- Explain WHY along with HOW

If you don’t know something:

> “I haven’t worked directly on it, but I understand the concept and can learn it quickly.”

That is a perfectly acceptable answer for a 2-year DevOps role.
