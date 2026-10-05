\# 🚀 DevOps Internship – Task 3



\# Infrastructure as Code (IaC) with Terraform



!\[Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC?style=for-the-badge\&logo=terraform\&logoColor=white)

!\[Docker](https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)

!\[Nginx](https://img.shields.io/badge/Nginx-Web%20Server-009639?style=for-the-badge\&logo=nginx\&logoColor=white)

!\[Windows](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge\&logo=windows\&logoColor=white)



\---



\## 📌 Task Overview



This project is part of my \*\*DevOps Internship – Task 3\*\*.



The objective of this task is to understand and implement \*\*Infrastructure as Code (IaC)\*\* using \*\*Terraform\*\* to provision and manage a local \*\*Docker container\*\*.



The Docker provider is configured in Terraform, an Nginx image is created, and an Nginx container is provisioned using Terraform.



\---



\## 🎯 Objective



> Provision a local Docker container using Terraform.



The project demonstrates the complete Terraform infrastructure lifecycle:



```text

Terraform Configuration

&#x20;       ↓

terraform init

&#x20;       ↓

terraform plan

&#x20;       ↓

terraform apply

&#x20;       ↓

Docker Container

&#x20;       ↓

Terraform State

&#x20;       ↓

terraform destroy

```



\---



\## 🛠️ Tools \& Technologies



\- Terraform

\- Docker Desktop

\- Docker Provider for Terraform

\- Nginx

\- Windows PowerShell

\- Git

\- GitHub



\---



\## 📂 Project Structure



```text

task-3-terraform/

│

├── main.tf

├── README.md

├── execution-logs.txt

│

└── screenshots/

&#x20;   ├── 01-terraform-init.png

&#x20;   ├── 02-terraform-plan.png

&#x20;   ├── 03-terraform-apply.png

&#x20;   ├── 04-docker-container.png

&#x20;   ├── 05-nginx-browser.png

&#x20;   ├── 06-terraform-state.png

&#x20;   ├── 07-terraform-show.png

&#x20;   └── 08-terraform-destroy.png

```



\---



\# 🏗️ Terraform Configuration



The main Terraform configuration is stored in:



```text

main.tf

```



The configuration uses the Docker provider and creates an Nginx Docker image and container.



\### `main.tf`



```hcl

terraform {

&#x20; required\_providers {

&#x20;   docker = {

&#x20;     source  = "kreuzwerker/docker"

&#x20;     version = "\~> 3.0"

&#x20;   }

&#x20; }

}



provider "docker" {}



resource "docker\_image" "nginx" {

&#x20; name = "nginx:latest"

}



resource "docker\_container" "nginx" {

&#x20; name  = "terraform-nginx"

&#x20; image = docker\_image.nginx.image\_id



&#x20; ports {

&#x20;   internal = 80

&#x20;   external = 8080

&#x20; }

}

```



\---



\# 🔍 Configuration Explanation



\## 1. Terraform Block



```hcl

terraform {

&#x20; required\_providers {

&#x20;   docker = {

&#x20;     source  = "kreuzwerker/docker"

&#x20;     version = "\~> 3.0"

&#x20;   }

&#x20; }

}

```



This specifies the Docker provider required by Terraform.



\---



\## 2. Docker Provider



```hcl

provider "docker" {}

```



This tells Terraform to use Docker for managing the infrastructure.



\---



\## 3. Docker Image



```hcl

resource "docker\_image" "nginx" {

&#x20; name = "nginx:latest"

}

```



This defines the Nginx Docker image that Terraform will manage.



\---



\## 4. Docker Container



```hcl

resource "docker\_container" "nginx" {

&#x20; name  = "terraform-nginx"

&#x20; image = docker\_image.nginx.image\_id

```



This creates a Docker container using the Nginx image.



\---



\## 5. Port Mapping



```hcl

ports {

&#x20; internal = 80

&#x20; external = 8080

}

```



The Nginx container listens on port `80`.



It is exposed on the host through port `8080`.



```text

localhost:8080

&#x20;      ↓

Docker Container

&#x20;      ↓

Nginx Port 80

```



\---



\# 🚀 Implementation Steps



\## Step 1 – Verify Terraform



```powershell

terraform version

```



Example:



```text

Terraform v1.13.4

on windows\_amd64

```



\---



\## Step 2 – Verify Docker



```powershell

docker --version

```



Then:



```powershell

docker ps

```



Docker Desktop must be running before Terraform creates the container.



\---



\# Step 3 – Initialize Terraform



Run:



```powershell

terraform init

```



Terraform downloads and initializes the Docker provider.



\### Screenshot



!\[Terraform Init](screenshots/01-terraform-init.png)



\---



\# Step 4 – Format Terraform Configuration



Run:



```powershell

terraform fmt

```



This formats the Terraform configuration.



\---



\# Step 5 – Validate Configuration



Run:



```powershell

terraform validate

```



Expected result:



```text

Success! The configuration is valid.

```



\---



\# Step 6 – Create Terraform Plan



Run:



```powershell

terraform plan

```



Terraform shows the resources that will be created.



Expected result:



```text

Plan: 2 to add, 0 to change, 0 to destroy.

```



The two resources are:



```text

docker\_image.nginx

docker\_container.nginx

```



\### Screenshot



!\[Terraform Plan](screenshots/02-terraform-plan.png)



\---



\# Step 7 – Apply Terraform Configuration



Run:



```powershell

terraform apply

```



Enter:



```text

yes

```



Terraform creates:



1\. Nginx Docker image

2\. Nginx Docker container



Expected result:



```text

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

```



\### Screenshot



!\[Terraform Apply](screenshots/03-terraform-apply.png)



\---



\# Step 8 – Verify Docker Container



Run:



```powershell

docker ps

```



The Terraform-created container should be running.



Example:



```text

CONTAINER ID   IMAGE          PORTS                  NAMES

xxxxxxxxxxxx   nginx:latest   0.0.0.0:8080->80/tcp   terraform-nginx

```



\### Screenshot



!\[Docker Container](screenshots/04-docker-container.png)



\---



\# Step 9 – Test Nginx in Browser



Open:



```text

http://localhost:8080

```



The Nginx welcome page should appear.



Expected result:



```text

Welcome to nginx!



If you see this page, nginx is successfully installed and working.

```



\### Screenshot



!\[Nginx Browser](screenshots/05-nginx-browser.png)



\---



\# Step 10 – Check Terraform State



Run:



```powershell

terraform state list

```



Expected:



```text

docker\_container.nginx

docker\_image.nginx

```



This shows the resources currently managed by Terraform.



\### Screenshot



!\[Terraform State](screenshots/06-terraform-state.png)



\---



\# Step 11 – Display Terraform State Details



Run:



```powershell

terraform show

```



This displays detailed information about the Terraform-managed infrastructure.



\### Screenshot



!\[Terraform Show](screenshots/07-terraform-show.png)



\---



\# Step 12 – Destroy Infrastructure



After completing the verification, destroy the infrastructure using:



```powershell

terraform destroy

```



Enter:



```text

yes

```



Terraform removes the Docker resources it created.



Expected result:



```text

Destroy complete! Resources: 2 destroyed.

```



\### Screenshot



!\[Terraform Destroy](screenshots/08-terraform-destroy.png)



\---



\# 📊 Task Execution Summary



| Operation | Command | Result |

|---|---|---|

| Initialize | `terraform init` | ✅ Successful |

| Format | `terraform fmt` | ✅ Successful |

| Validate | `terraform validate` | ✅ Successful |

| Plan | `terraform plan` | ✅ 2 resources planned |

| Create | `terraform apply` | ✅ 2 resources created |

| Verify Docker | `docker ps` | ✅ Container running |

| Test Application | `localhost:8080` | ✅ Nginx working |

| Check State | `terraform state list` | ✅ Resources listed |

| Show State | `terraform show` | ✅ Resource details displayed |

| Destroy | `terraform destroy` | ✅ Resources removed |



\---



\# 📸 Execution Screenshots



\## 1. Terraform Initialization



!\[Terraform Init](screenshots/01-terraform-init.png)



\---



\## 2. Terraform Plan



!\[Terraform Plan](screenshots/02-terraform-plan.png)



\---



\## 3. Terraform Apply



!\[Terraform Apply](screenshots/03-terraform-apply.png)



\---



\## 4. Docker Container



!\[Docker Container](screenshots/04-docker-container.png)



\---



\## 5. Nginx Application



!\[Nginx Browser](screenshots/05-nginx-browser.png)



\---



\## 6. Terraform State



!\[Terraform State](screenshots/06-terraform-state.png)



\---



\## 7. Terraform Show



!\[Terraform Show](screenshots/07-terraform-show.png)



\---



\## 8. Terraform Destroy



!\[Terraform Destroy](screenshots/08-terraform-destroy.png)



\---



\# 📝 Execution Commands



The following commands were used during the task:



```powershell

terraform version



docker --version



docker ps



terraform init



terraform fmt



terraform validate



terraform plan



terraform apply



docker ps



terraform state list



terraform show



terraform destroy



docker ps

```



\---



\# 🧠 Key Concepts Learned



\## Infrastructure as Code



Infrastructure as Code (IaC) means defining and managing infrastructure using configuration files instead of manually creating resources.



In this project, Terraform configuration was used to define Docker infrastructure.



\---



\## Terraform Provider



A provider allows Terraform to interact with a specific platform or service.



This project uses:



```text

kreuzwerker/docker

```



to interact with Docker.



\---



\## Terraform State



Terraform maintains a state file to keep track of resources managed by Terraform.



The state can be inspected using:



```powershell

terraform state list

```



and:



```powershell

terraform show

```



\---



\## Terraform Plan



```powershell

terraform plan

```



shows the changes Terraform intends to make without applying them.



\---



\## Terraform Apply



```powershell

terraform apply

```



actually creates or modifies the infrastructure defined in the Terraform configuration.



\---



\## Terraform Destroy



```powershell

terraform destroy

```



removes infrastructure managed by Terraform.



\---



\# 🔐 Security Notes



Terraform state files can contain sensitive information in real-world projects.



For this simple project, the repository should avoid committing sensitive credentials or secrets.



Recommended `.gitignore`:



```gitignore

.terraform/

\*.tfstate

\*.tfstate.\*

crash.log

crash.\*.log

\*.tfvars

\*.tfvars.json

```



The Terraform dependency lock file should be kept:



```text

.terraform.lock.hcl

```



\---



\# 📌 Result



The task successfully demonstrated Infrastructure as Code using Terraform and Docker.



Terraform was used to:



```text

Create Docker Image

&#x20;       ↓

Create Docker Container

&#x20;       ↓

Expose Nginx on Port 8080

&#x20;       ↓

Verify Application

&#x20;       ↓

Inspect Terraform State

&#x20;       ↓

Destroy Infrastructure

```



The Nginx web server was successfully accessed through:



```text

http://localhost:8080

```



\---



\# 👨‍💻 Author



\*\*Vinayak Raval\*\*



DevOps / Cloud Enthusiast  

B.E. Computer Science \& Engineering



\---



\# ⭐ Internship Task



\*\*DevOps Internship – Task 3\*\*



\*\*Topic:\*\* Infrastructure as Code (IaC) with Terraform



\*\*Tools:\*\* Terraform + Docker



\*\*Objective:\*\* Provision a local Docker container using Terraform.



\---

