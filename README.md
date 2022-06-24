
# Deploying Baselab Namespace and Services
The steps outline below assume you have a Kubernetes environment up and running.  If you do not have a ready environment you can use the [K8S via Ansible](https://github.com/CHernandezNY/k8s-ansible) or [K3s via Ansible](https://github.com/CHernandezNY/k3s-ansible) to build a quick lab .

## Deploy Baselab Applications 
Start provisioning of the cluster using the following command:

``
$ ansible-playbook deployments.yml -i inventory/hosts.ini
``  
## Applications 
The deployment sets up a namespace called baselab that contains five (5) applications I find the most useful in my lab.

### NGINX 
This lab contains four (4) instances of NGINX web servers, RED, GREEN, BLUE and RGB.  These are useful for testing traffic policies, scripts, ingress policies, and all around simple web content server.  
![NGINX RGB](https://github.com/CHernandezNY/pcl-baselab/blob/main/images/nginx-rgb.jpg)

### Echo Server 
Web server that echos back the HTTP request sent.  This is especially useful when testing header insertions. request manipulation through BIG-IP iRules, Access Policies or NGINX Proxy rules.
![Echo Server](https://github.com/CHernandezNY/pcl-baselab/blob/main/images/echoserver.jpg)

### Juice Shop
Juice Shop encompasses vulnerabilities from the entire OWASP Top Ten along with many other security flaws found in real-world applications.  It can be used in testing BIG-IP Advance WAF, NGINX App Protect, security trainings, or awareness demos.
![Juice Shop](https://github.com/CHernandezNY/pcl-baselab/blob/main/images/juiceshop.jpg)

### Keycloak
Keycloak is an open source software product to allow single sign-on with Identity and Access Management. It can be set up as a OpenID Connect or SAML 2.0 Identity Providers. Great for testing OAuth and SAML configurations with BIG-IP APM.
![Keycloak](https://github.com/CHernandezNY/pcl-baselab/blob/main/images/keycloak.jpg)

### PiHole 
General purpose DNS server.  Provides UDP and TCP DNS listeners and HTTP webUI.  
![PiHole](https://github.com/CHernandezNY/pcl-baselab/blob/main/images/pihole.jpg)

## Exposing Applications via Services
In the k8s_yamls/services folder are some example for exposing the applications as with Service  type ClusterIP or type LoadBalancer.  The ClusterIP sets up a internal load balancing service that is then exposed using NGINX Ingress Controller (KIC) or F5 Container Ingress Services (CIS). 
