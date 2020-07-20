# kube-certified-administrator-prep-guide
CKA preparation guide

Certified Kubernetes Administrator (CKA) - V1.18
The objective of this repository is help you for taking the Certified Kubernetes Administrator (CKA) exam using online resources, especially using resources from Kubernetes Official Documentation.

The references were selected for the Exam Curriculum 1.18, which uses Kubernetes 1.18 version, and there are exclusive information for API objects and annotations. For more information, please see CKA Curriculum.

Please, feel free to place a pull request whether something is not up-to-date, should be added or contains wrong information/reference.

Exam
The exam is kind of "put your hands on", where you have 24 problems to fix within 180 minutes. Based on that, you have ~7.5 minutes per problem, where usually you will spend more time in some problems than others.

My tip: Spend your time wisely. Use the Notebook feature (provided in exam's UI) to keep track of your progress, where you might take notes of each question, put some annotations in order to help you. Additionally, don't get stuck, move to the next problem, and take it back when you finish all the other problems.

Exam Cost: $300 and includes one free retake.

It's important to mention that you have access to Kubernetes Official Documentation during the exam. So get yourself familiar with Kubernetes online documentation, and know where to find all specific topics listed below. It might be helpful for you during the exam.

For information about the exam, please refer Certified Kubernetes Administrator (CKA) Program.

CKA Curriculum
Exam objectives that outline of the knowledge, skills and abilities that a Certified Kubernetes Administrator (CKA) can be expected to demonstrate.

Application Lifecycle Management 8%
Understand Deployments and how to perform rolling updates and rollbacks.

Concepts: Workloads: Controllers: Deployment

Example Deployment File (dep-nginx.yaml) using NGINX

apiVersion: apps/v1
kind: Deployment
metadata:
    name: nginx-deployment
    labels:
        app: nginx
spec:
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
        image: nginx:1.15.4
        ports:
        - containerPort: 80
# Create Deployment
kubectl create -f dep-nginx.yaml

# Get Deployments
kubectl get deployments

# Update Deployment
kubectl edit deployment.v1.apps/nginx-deployment

# See rollout status
kubectl rollout status deployment.v1.apps/nginx-deployment

# Describe Deployment
kubectl describe deployment

# Rolling back to a previous revision
kubectl rollout undo deployment.v1.apps/nginx-deployment
Know various ways to configure applications.

Concepts: Cluster Administration: Managing Resources
Know how to scale applications.

Concepts: Cluster Administration: Managing Resources: #Scaling Your Application.

# Increase replicas number for nginx-deployment
kubectl scale deployment/nginx-deployment --replicas=5

# Using autoscaling
kubectl autoscale deployment/nginx-deployment --min=2 --max=5
Understand the primitives necessary to create a self-healing application.

Concepts: Workloads: Pods: Pod Lifecycle

Tasks: Configure Pods and Containers: Liveness and Readiness Probes

Installation, Configuration & Validation 12%
Design a Kubernetes cluster.

Concepts: Cluster Administration: Overview: Planning a Cluster
Install Kubernetes masters and nodes.

Getting Started: Production environment: Bootstrapping Clusters with kubeadm: Creating Highly Available clusters with kubeadm
Configure secure cluster communications.

Tasks: TLS: Manage TLS Certificates in a Cluster
Configure a Highly-Available Kubernetes cluster.

Getting Started: Production environment: Bootstrapping Clusters with kubeadm: Creating Highly Available Clusters with kubeadm
Know where to get the Kubernetes release binaries.

Getting Started: Release Notes
Provision underlying infrastructure to deploy a Kubernetes cluster.

Getting Started
Choose a network solution.

Getting Started: Production environment: Bootstrapping Clusters with kubeadm: Creating a single master cluster with kubeadm: #Installing a pod network add-on
Choose your Kubernetes infrastructure configuration.

Getting Started: Production environment: Bootstrapping Clusters with kubeadm: Options for Highly Available topology
Run end-to-end tests on your cluster.

Reference: Kubectl Commands: Cluster Management

Extra: End-to-End Testing in Kubernetes

Analyse end-to-end tests results.

Extra: Kubetest
Run Node end-to-end tests.

Node End-To-End tests
Install and use kubeadm to install, configure, and manage Kubernetes cluster.

Getting started: Production environment: Installing Kubernetes with deployment tools: Bootstrapping clusters with kubeadm
# Display addresses of the master and services
kubectl cluster-info

# Dump current cluster state to stdout
kubectl cluster-info dump

# Check health of cluster components
kubectl get componentstatuses

# List the nodes
kubectl get nodes

# Show metrics for a given node
kubectl top node my-node

# List all pods in all namespaces, with more details
kubectl get pods -o wide --all-namespaces

# List all services in all namespaces, with more details
kubectl get svc  -o wide --all-namespaces
Core Concepts 19%
Understand the Kubernetes API primitives

Concepts: Kubernetes API Overview
Concepts: Understanding Kubernetes Objects.
Reference: Kubernetes API Reference
Optional: Kubernetes Architecture 101 (Video Youtube)
Understand the Kubernetes cluster architecture.

Concepts: Kubernetes Components
Concepts: Concepts Underlying the Cloud Controller Manager
Understand Services and other network primitives.

Concepts: Services, Load Balancing and Networking
Networking 11%
Understand the networking configuration on the cluster nodes.

Concepts: Cluster Administration: Cluster Networking
Understand Pod networking concepts.

Kubernetes Project: Design Proposals - Network
Understand service networking.

Concepts: Services, Load Balancing, and Networking: Services
Deploy and configure network load balancer.

Tasks: Access Applications in a Cluster: Create an External Load Balancer
Know how to use Ingress rules.

Concepts: Services, Load Balancing, and Networking: Ingress
Know how to configure and use the cluster DNS.

Concepts: Services, Load Balancing, and Networking: DNS for Services and Pods
Understand CNI.

Concepts: Extending Kubernetes: Compute, Storage, and Networking Extensions: Network Plugins
Scheduling 5%
Use label selectors to schedule Pods.

Concepts: Overview: Working with Kubernetes Objects: Labels and Selectors
Understand the role of DaemonSets.

Concepts: Workloads: Controllers: DaemonSet
Understand how resource limits can affect Pod scheduling.

Tasks: Administer a Cluster: Manage Memory, CPU, and API Resources: Configure Default Memory Requests and Limits for a Namespace
Tasks: Administer a Cluster: Manage Memory, CPU, and API Resources: Configure Default CPU Requests and Limits for a Namespace
Understand how to run multiple schedulers and how to configure Pods to use them.

Tasks: Administer a Cluster: Configure Multiple Schedulers
Manually schedule a pod without a scheduler.

Tasks: Administer a Cluster: Static Pods
Dispaly scheduler events.

Tasks: Administer a Cluster: Configure Multiple Schedulers: #Verifying that the pods were scheduled using the desired schedulers

$ kubectl get events
# or
$ kubectl describe pods | grep -A7 ^Events

# Master/Control node 
$ tail /var/log/kube-scheduler.log
Know how to configure the Kubernetes scheduler.

Tasks: Administer a Cluster: Configure Multiple Schedulers
Security 12%
Know how to configure authentication and authorization.

Tasks: Administer a Cluster: Securing a Cluster
Understand Kubernetes security primitives.

Reference: Accessing the API: Authorization Overview
Check all sub resources (Node Authorization, ABAC, RBAC, and Webhook)
Know to configure network policies.

Tasks: Administer a Cluster: Declare Network Policy
Create and manage TLS certificates for cluster components.

Tasks: TLS: Manage TLS Certificates in a Cluster
Work with images securely.

Concepts: Containers: Images

Concepts: Configuration: Best Practices: #Container Images

Define security contexts.

Tasks: Configure Pods and Containers: Configure a Security Context for a Pod or Container
Secure persistent key value store.

Concepts: Configuration: Secrets
Cluster Maintenance 11%
Understand Kubernetes cluster upgrade process.

Tasks: Administer a Cluster: Administration with kubeadm: Upgrading kubeadm clusters
Facilitate operating system upgrades.

Implement backup and restore methodologies.

Tasks: Administer a Cluster: Operating etcd clusters for Kubernetes
Logging / Monitoring 5%
Understand how to monitor all cluster components.

Tasks: Monitor, Log, and Debug: Tools for Monitoring Resources
Understand how to monitor applications.

Tasks: Monitor, Log, and Debug: Application Introspection and Debugging
Manage cluster component logs.

Tasks: Monitor, Log, and Debug: Troubleshoot Clusters

Master Log Files
/var/log/kube-apiserver.log - API Server, responsible for serving the API
/var/log/kube-scheduler.log - Scheduler, responsible for making scheduling decisions
/var/log/kube-controller-manager.log - Controller that manages replication controllers
Worker Nodes Log Files
/var/log/kubelet.log - Kubelet, responsible for running containers on the node
/var/log/kube-proxy.log - Kube Proxy, responsible for service load balancing
Manage application logs.

Tasks: Monitor, Log, and Debug: Troubleshoot Applications
Storage 7%
Understand persistent volumes and know how to create them.

Concepts: Storage: Persistent Volumes
Understand access modes for volumes.

Concepts: Storage: Persistent Volumes: #Access Modes
Understand persistent volume claims primitive.

Concepts: Storage: Persistent Volumes: #PersistentVolumeClaims
Understand Kubernetes storage objects.

Concepts: Storage: Volumes
Know how to configure applications with persistent storage.

Concepts: Storage: Volumes: #local
Concepts: Storage: Volumes: #hostPath
Troubleshooting 10%
Troubleshoot application failure.

Tasks: Monitor, Log, and Debug: Troubleshoot Applications
Tasks: Monitor, Log, and Debug: Determine the Reason for Pod Failure
Troubleshoot control plane failure.

Tasks: Monitor, Log, and Debug: Troubleshoot Clusters
Troubleshoot worker node failure.

Tasks: Monitor, Log, and Debug: Troubleshoot Clusters: #Worker Nodes
Troubleshoot networking.

CKA Preparation Courses
Certified Kubernetes Administrator (CKA) - Linux Academy

Kubernetes Fundamentals (LFS258) - Linux Foundation

Kubernetes Deep Dive - A Cloud Guru

kubectl Ninja
Tip: Use kubectl Cheatsheet during the exam. You don't need to decorate everything.

Useful commands or parameters during the exam:
# Use "kubectl describe" for related events and troubleshooting
kubectl describe pods <podid>

# Use "kubectl explain" to check the structure of a resource object.
kubectl explain deployment --recursive

## Add "-o wide" in order to use wide output, which gives you more details.
kubectl get pods -o wide

## Check always all namespaces by including "--all-namespaces"
kubectl get pods --all-namespaces
Generate a manifest template from imperative spec using the output option "-o yaml" and the parameter "--dry-run":

# create a service
kubectl create service clusterip my-service --tcp=8080 --dry-run -o yaml

# create a deployment
kubectl create deployment nginx --image=nginx --dry-run -o yaml

# create a pod
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml
Create resources using kubectl + stdin instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

cat <<EOF | kubectl create -f -
...
EOF  
It saves lots of time, believe me.

Kubectl Autocomplete

source <(kubectl completion bash)
Practice
Practice a lot with Kubernetes:

Kubernetes the Hard Way by Kelsey Hightower
Katacoda: Learn Kubernetes using Interactive Browser-Based Scenarios
CKA Tips
Some links that contain tips that might help you from different perspectives of the CKA exam.

Graham Moore - 7.5 tips to help you ace the Certified Kubernetes Administrator (CKA) exam
How to pass the Certified Kubernetes Administrator (CKA) exam on the first attempt
