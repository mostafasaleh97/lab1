# TeamStack Project

👋 **Hello and Welcome to TeamStack!** 👋

We're thrilled to have you here! TeamStack is your dedicated partner for effortlessly creating and automating the installation of a powerful cluster using Terraform and Ansible.

## Overview

This project has been crafted to simplify your cluster deployment experience, whether you're a seasoned developer or just getting started. TeamStack empowers you to seamlessly set up and manage your clusters, providing a solid foundation for your applications.

## Key Features
- **Automation:** TeamStack utilizes the combined strength of Terraform and Ansible to automate the deployment process, ensuring a smooth and efficient cluster creation.
- **Scalability:** Easily scale your infrastructure up or down, adapting to the dynamic needs of your applications.
- **Flexibility:** Tailor your cluster configuration to suit your specific requirements and preferences.
- **Comprehensive Documentation:** Our detailed documentation guides you through each step, guaranteeing a hassle-free installation and configuration process.

Let's embark on a journey to create, manage, and optimize your clusters effortlessly with TeamStack!
## OpenStack Overview

Welcome to the world of OpenStack! An open-source cloud computing platform designed to simplify the deployment and management of both public and private clouds. OpenStack offers a suite of services, including computing, storage, and networking, making it a versatile choice for diverse cloud infrastructure needs.

### Streamlining Deployment with Automation

TeamStack embraces the power of automation to enhance the efficiency of OpenStack infrastructure deployment. By employing tools like Terraform and Ansible, we can simplify and expedite the process of creating and configuring resources on OpenStack.

#### Terraform: Infrastructure as Code (IaC)

[Terraform](https://www.terraform.io/) acts as our Infrastructure as Code (IaC) tool, allowing you to define and provision infrastructure in a declarative manner. This empowers you to efficiently manage your infrastructure through code, providing consistency and reproducibility.

#### Ansible: Automation for Configuration Management

[Ansible](https://www.ansible.com/) complements Terraform by automating configuration management. With Ansible, you can define tasks and roles in a human-readable format, ensuring consistent and repeatable configurations across your OpenStack instances.

### Getting Started: A Simple Example

To illustrate the power of automation, we'll walk you through a basic scenario using Terraform and Ansible. This simple example involves deploying instances on OpenStack and configuring them using Ansible. While straightforward, it lays the groundwork for more complex configurations tailored to your specific needs.

## Terraform Configuration Overview

In this section, we will explore the Terraform configuration used in the TeamStack project. The Terraform configuration is divided into three main files, each serving a specific purpose.

### 1. Provider Configuration (`provider.tf`)

The `provider.tf` file contains OpenStack provider configuration details, including the authentication URL, project name, and credentials.

### 2. Network Configuration (`network.tf`)

The `network.tf` file is responsible for creating essential network resources:

- **Network:** A private network where the cluster will be installed.
- **Subnet:** A private CIDR in the network (e.g., `192.168.1.0/24`). Here, a single subnet is created, but you can customize this for more complex setups.
- **Port:** Used to reserve an IP for each resource in the network. Six ports are utilized for six instances, enabling the allocation of floating IPs for external access.
- **Floating IP:** An IP assigned to instances for external accessibility.
- **Route:** Creates a router in the external network to access the internet and establishes a route interface between the router and the private network, enabling communication.

**Note:** Each instance will have two IPs - a private IP from the subnet CIDR and a public IP (floating IP).

- **Security Group:** Defines the necessary rules and ports for secure communication on instances.

### 3. Instance Configuration (`instance.tf`)

The `instance.tf` file is responsible for creating instances where the Kubernetes cluster will be deployed. Two instances serve as master nodes, and the remaining instances function as worker nodes.

### Getting Started

Follow these steps to use Terraform for deploying the infrastructure:

1. **Install Terraform:**
    ```bash
    # For Linux
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-keyring.gpg
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list > /dev/null
    sudo apt-get update && sudo apt-get install terraform

    # For macOS
    brew install hashicorp/tap/terraform

    # For Windows (using PowerShell)
    # choco install terraform
    ```

2. **Run Terraform Commands:**
    ```bash
    cd ./terraform
    terraform init
    terraform apply --auto-approve
    ```

These commands initialize Terraform and create the specified resources on your OpenStack platform. The `--auto-approve` flag skips the confirmation prompt for a smooth, automated process.

The Terraform configuration provided is designed for a simple demonstration, laying the foundation for more advanced use cases based on your specific requirements.

Continue to the next section where we'll dive into Ansible to automate the configuration of these instances.

## Ansible: Automation with Ease

### Installing Ansible

Follow these steps to install Ansible:

#### For Linux
```bash
sudo apt-get update
sudo apt-get install ansible

Build a Kubernetes cluster using RKE2 via Ansible
=========
```
               ,        ,  _______________________________
   ,-----------|'------'|  |                             |
  /.           '-'    |-'  |_____________________________|
 |/|             |    |
   |   .________.'----'    _______________________________
   |  ||        |  ||      |                             |
   \__|'        \__|'      |_____________________________|

|‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾|
|________________________________________________________|

|‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾‾|
|________________________________________________________|
```

Ansible RKE2 (RKE Government) Playbook
---------
[![LINT](https://github.com/rancherfederal/rke2-ansible/actions/workflows/ci.yml/badge.svg)](https://github.com/rancherfederal/rke2-ansible/actions/workflows/ci.yml)

RKE2, also known as RKE Government, is Rancher's next-generation Kubernetes distribution. This Ansible  playbook installs RKE2 for both the control plane and workers.

See the [docs](https://docs.rke2.io/) more information about [RKE Government](https://docs.rke2.io/).


Platforms
---------
The RKE2 Ansible playbook supports all [RKE2 Supported Operating Systems](https://docs.rke2.io/install/requirements/#operating-systems)

Supported Operating Systems:
```yaml
SLES:
  - 15 SP2 (amd64)
CentOS:
  - 7.8 (amd64)
  - 8.2 (amd64)
Red Hat:
  - 7.8 (amd64)
  - 8.2 (amd64)
Ubuntu:
  - bionic/18.04 (amd64)
  - focal/20.04 (amd64)
```


System requirements
-------------------

Deployment environment must have Ansible 2.9.0+

Server and agent nodes must have passwordless SSH access

Usage
-----

This playbook requires ansible.utils to run properly. Please see https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#installing-a-collection-from-galaxy for more information about how to install this.

```
ansible-galaxy collection install -r requirements.yml
```

Create a new directory based on the `sample` directory within the `inventory` directory:

```bash
cp -R inventory/sample inventory/my-cluster
```

Second, edit `inventory/my-cluster/hosts.ini` to match the system information gathered above. For example:

```bash
[rke2_servers]
192.16.35.12

[rke2_agents]
192.16.35.[10:11]

[rke2_cluster:children]
rke2_servers
rke2_agents
```

If needed, you can also edit `inventory/my-cluster/group_vars/rke2_agents.yml` and `inventory/my-cluster/group_vars/rke2_servers.yml` to match your environment.

Start provisioning of the cluster using the following command:

```bash
ansible-playbook site.yml -i inventory/my-cluster/hosts.ini
```

Tarball Install/Air-Gap Install
-------------------------------
Added the neeed files to the [tarball_install](tarball_install/) directory.

Further info can be found [here](tarball_install/README.md)


Kubeconfig
----------

To get access to your **Kubernetes** cluster just

```bash
ssh ubuntu@kubernetes_api_server_host "sudo /var/lib/rancher/rke2/bin/kubectl --kubeconfig /etc/rancher/rke2/rke2.yaml get nodes"
```

Available configurations
------------------------

Variables should be set in `inventory/cluster/group_vars/rke2_agents.yml` and `inventory/cluster/group_vars/rke2_servers.yml`. See sample variables in `inventory/sample/group_vars` for reference.


Uninstall RKE2
---------------
    Note: Uninstalling RKE2 deletes the cluster data and all of the scripts.
The offical documentation for fully uninstalling the RKE2 cluster can be found in the [RKE2 Documentation](https://docs.rke2.io/install/uninstall/).

If you used this module to created the cluster and RKE2 was installed via yum, then you can attempt to run this command to remove all cluster data and all RKE2 scripts.

Replace `ubuntu` with your ansible user.
```bash
ansible -i floating-ip, all -u ubuntu -a "/usr/bin/rke2-uninstall.sh"
```

If the tarball method was used then you can attempt to use the following command:
```bash
ansible -i floating-ip, all -u ubuntu -a "/usr/local/bin/rke2-uninstall.sh"
```
On rare occasions you may have to run the uninstall commands a second time.

Known Issues
------------------
- For RHEL8+ Operating Systems that have fapolicyd daemon running, rpm installation of RKE2 will fail due to a permission error while starting containerd. Users have to add the following rules file before installing RKE2. This is not an issue if the install.sh script is used to install RKE2. The RPM issue is expected to be fixed in later versions of RKE2.
```bash
cat <<-EOF >>"/etc/fapolicyd/rules.d/80-rke2.rules"
allow perm=any all : dir=/var/lib/rancher/
allow perm=any all : dir=/opt/cni/
allow perm=any all : dir=/run/k3s/
allow perm=any all : dir=/var/lib/kubelet/
EOF

systemctl restart fapolicyd

```


