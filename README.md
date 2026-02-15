Roboshop Deployment using Ansible Roles

Project Overview
This project automates the deployment of the Roboshop microservices application using Ansible Roles.
Roboshop is a cloud-native e-commerce application with multiple microservices like frontend, catalogue, cart, user, shipping, payment, and database services.
Tech Stack
* Ansible (Configuration Management)
* AWS EC2 (Infrastructure)
* Linux (RHEL)
* Node.js, Java, Python (Application services)
* MongoDB, MySQL, Redis,Rabbitmq (Databases)
* Nginx (Frontend)

1. Prerequisites (Manual Setup)
Before running the automation, you must manually set up a Management Node (Ansible Control Plane).
Launch an EC2 Instance.
Install Ansible:
sudo dnf install ansible -y

Configure AWS CLI:
Ensure the instance has the necessary IAM permissions or configure your credentials manually:
aws configure
Provide Access Key, Secret Key, and Default Region (e.g., us-east-1)

Use code with caution.

🏗️ Project Structure
ansible-roboshop-roles/
│
├── ansible.cfg
├── inventory.ini
├── roboshop.yaml
├── group_vars/
│
└── roles/
    ├── cart/
    ├── catalogue/
    │   ├── files/
    │   ├── meta/
    │   ├── tasks/
    │   ├── templates/
    │
    ├── common/
    │   └── tasks/
    │
    ├── frontend/
    ├── mongodb/
    ├── mysql/
    ├── payment/
    ├── rabbitmq/
    ├── redis/
    ├── shipping/
    ├── user/
 ⚙️ Ansible Configuration

--> ansible.cfg


[defaults]
inventory = inventory.ini
log_path = ./ansible.log

Roles Description

| Role      | Description                          |
| --------- | ------------------------------------ |
| common    | Common setup (users, dependencies)   |
| frontend  | Nginx + UI deployment                |
| catalogue | Node.js service + MongoDB connection |
| cart      | Node.js cart service                 |
| user      | User service                         |
| shipping  | Java + Maven service                 |
| payment   | Python service                       |
| mongodb   | MongoDB installation & schema        |
| mysql     | MySQL setup for shipping             |
| redis     | Redis cache setup                    |
rabbitmq    | Messaging queue                      |

---

▶️ Playbook Execution

Run specific role
ansible-playbook -e component=catalogue roboshop.yaml 

🔧 Key Features

* Modular design using Ansible Roles
* Idempotent automation
* Easy scalability for microservices
* Environment-specific inventory support
* Centralized configuration

---

🐞 Troubleshooting


  DBs only need Port Checks
   
    databases:
      mongodb: 27017
      redis: 6379
      mysql: 3306
      rabbitmq: 5672

    #Apps need HTTP Health Checks
    apps:
      catalogue: 8080
      user: 8080
      cart: 8080
      shipping: 8080
      payment: 8080
      frontend: 80

1. Connection Refused (Port Issue)
 Check service status:
netstat -lntp
systemctl status <service>
2. Service Not Starting
Check logs:
journalctl -u <service> -f
3. Inventory Not Working
ansible-inventory --list
4. Permission Issues
* Ensure log_path is writable

🧠 Learnings
* Hands-on experience with Ansible roles
* Real-time DevOps troubleshooting
* Microservices deployment automation
* Infrastructure + application integration
Future Enhancements

* CI/CD integration (Jenkins)
* Terraform for infra provisioning
* Kubernetes deployment
* Monitoring setup (Prometheus, Grafana)

---



