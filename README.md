# Overview
This terraform code can help yopu manage your automate cluster frontend configuration.

#### Supported platforms:
 * Linux

## Prerequisites
You will need the access details for an automate cluster. 
* user name for ssh
* ssh private key for the ssh user access
* ip address for chef server frontends
* ip address for automate frontends
* if needed the ssh users sudo password
* chef server config toml file
* automate server config toml file

The module will ssh into each of the chef server and / or automate server ip addresses and write the relevent configuration file, and then run chef-automate config patch on that configuration file.

## Usage
In the root of the terraform_11 or terraform_12 directory will be a file named `terraform.tfvars.example` copy this file to one called `terraform.tfvars`. Then enter all of the required values to the variables.

```bash
cp terraform.tfvars.example terraform.tfvars
```
After you have filled in the values to `terrafrom.tfvars` it should look similar to the content below.
```hcl

a2_cluster_ssh_key = "~/.ssh/my_key"
a2_cluster_ssh_user = "centos"
a2_cluster_sudo_pass = "mysudopass"

existing_chef_server_ips = ["172.16.1.10","172.16.1.11","172.16.1.12"]
existing_automate_ips = ["172.16.1.20","172.16.1.21","172.16.1.22"]

chef_server_config_file = "/tmp/my_chef_config"
automate_config = "/tmp/my_automate_config"
```

## Full List of Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
|a2_cluster_ssh_user|The user name to use for ssh connections|string||yes|
|a2_cluster_ssh_key|The path to an ssh private key to use for ssh connections|string||yes|
|a2_cluster_sudo_pass|Password for sudo elevation if the ssh user needs it|string|""|no|
|existing_chef_server_ips|A list containing the ip addresses of the chef server frontends|list||yes|
|existing_automate_ips|A list containing the ip addresses of the automate frontends|list||yes|
|chef_server_config_file|The path to a file containing the chef server toml config |string||yes|
|automate_config_file|The path to a file containing the automate toml config |string||yes|

## Running
Once you have configured your input variables into the `terraform.tfvars` file, run the follwoing commands to apply your config to the cluster frontends:
``` bash
terraform init
terraform plan
terraform apply
```

### Output
After the terrafrom has finished runnig you should see the config that was applied as output
