-> Anthos is an application management platform for cloud and on-prem environments

Components of Anthos
********************
1. Google Kubernetes Engine
2. GKE On-Prem (Beta)
3. GCP Marketplace (Beta)
4. Anthos Config Management (Beta)
5. GKE Hub (Alpha)
6. Cloud Service Mesh (Alpha)

Compute Environment
*******************
-> Primary computing environment for Anthos relies on GKE to manage kubernetes installations
-> Offers upstream kubernetes releases and provide management capabilities for creating, scaling and upgrading clusters
-> Kubernetes has control plane and node plane
-> GKE hosts control plane and kube-apiserver is only accessible to customers
-> GKE manages node components using instances in Compute Engine

Networking Environment
**********************
-> Cloud VPN is used to connect on-prem environments to GCP
-> Kuberenetes allows users to provision Layer 4 and Layer 7 load balancers
-> GKE uses Network load balancing for Layer 4 and HTTP(S) load balancing for Layer 7 (Both are managed services)


Service Management
******************
-> Services are composed of many Pods, which execute containers
-> Istio for service mesh
-> Istio uses side car proxies to enhance network security, reliability and visibility; These functions are implemented in a seperate container in the same pod
-> Istio offers 
1. Fine grained control of traffic
2. Resiliency (retries, failovers, circuit breakers and fault injection)
3. Pluggable policy layer and configuration API supporting access control and rate limiting
4. Automatic metrics logs and traces for all traffic within the cluster (ingress and egress)
5. Secure service-to-service communication with authentication and authorization based on service accounts
6. A/B testing, Canary rollouts, fault injection and rate limiting

-> Cloud Service Mesh manages Istio in both GKE and GKE On-Prem, no work involved with configuration, installation, upgrades etc.
-> CSM also provides
1. Telemetry (connections between services)
2. Managed certificates for internal services (service-to-service encryption, issuing and rotation of mTLS certs and keys)
3. Integration with Cloud Identity Aware Proxy
-> Stronger security using context-aware access

Centralized config management
*****************************
-> Anthos provides Configuration as code via Config Management which deploys anthos config management operator to your GKE cluster
-> Allows us to monitor and apply configuration changes detected in a Git repo
-> Uses namespaces, labels and annotations to determine how and where to apply the config changes to all kube clusters
-> The repo provides a versioned, secured and controlled single source of truth for all kube configurations
-> YAML/JSON applied via kubectl can be merged with Anthos config management operator

Anthos config management benefits
*********************************
1. Single source of truth, control and management
2. Avoids shadow ops, clusters drift out of sync due to manual changes
3. One step deployment across all clusters (Single git commit into multiple clusters); Rollback by reverting the change in Git
4. Inheritance model for applying changes (Namespace based configurations for all clusters)

-> GKE dashboard provides unified user interface
-> GKE dashboard provides secure console to view state of kubernetes clusters and workloads

To connect to the cluster
*************************
-> Deploy GKE Connect agent, which sets up a secure tunnel that allows GCP consoleto manage resources in the cluster
-> Restrict capabilities of agent using RBAC

Anthos for development benefits
*******************************
1. Git-compliant management and CI/CD workflows for configuration as well as code using Anthos Config Management
2. Code-free instrumentation of code using Istio and Stackdriver to provide uniform observability
3. Code-free protection of services using mTLS and throttling with CSM (Istio)
4. Support for Google Cloud Platform Marketplace to quickly and easily drop off-the-shelf products into clusters

Anthos for operations benefits
******************************
1. Offers centralized, efficient and templatized deployment and management of clusters
2. Single command deployment of new clusters with GKE (gkectl)
3. Centralized configuration management and compliance with configuration-as-code and Anthos Config Management
4. Simplified deployment and rollback with Git check-ins
5. Single pane of glass visibility across all clusters from infrastructure through to application performance and topology with Stackdriver and CSM (Istio)

Anthos for security
*******************
1. Centralized, auditable, and securable workflow using Git compliant configuration repos with Anthos Config Management
2. Compliance enforcement of cluster configurations using Namespaces and inherited config with Anthos Config Management
3. Code-free securing of microservices using Istio, providing in-cluster mTLS and certificate management
4. Built-in services protection using Istio throttling and routing

