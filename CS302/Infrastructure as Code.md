The practice of defining virtualised infrastructure in machine-readable files.
- Removes hardship and drudgery from the value stream (AWS GUI...)
- Equivalent infrastructure can be quickly spun up
	- Creating a staging env
	- Repeatable and consistent
- Documents your infrastructure in version-controlled files
# Categories
- Ad hoc scripts - e.g. Bash
- Configuration management tools - Chef, Puppet, Ansible
	- Focuses on installing / managing software on existing servers
- Provisioning tools - Terraform, CloudFormation, OpenStack Heat
	- Focuses on creating servers, brokers, security groups, etc, themselves
# Terraform
- Language for provisioning infrastructure
	- AWS, GCP, ..., Kubernetes
- Configuration files are declarative
- Applies CRUD on user's behalf to achieve the desired state
- Maintains a local snapshot of the remote infrastructure's state
	- Plans CRUD operations by comparing the configuration file against the local state
## Configuration Files (HCL)
![[week12_hcl_01.png]]
![[wk12_terraform_workflow_01.png]]
## Key Commands
- `terraform init`
	- Initialises the current working directory
	- Apply it in a directory containing .tf files
	- Prepares the files for use with Terraform
- `terraform fmt`
	- Formats .tf files
	- Ensures consistent style
- `terraform plan`
	- Reads state of remove objects (e.g. EC2 instance)
	- Updates the state locally
	- Compares the state with .tf files
	- Proposes change actions to achieve the desired configuration
- `terraform apply`
	- Generates a plan, then applies it
- `terraform show`
	- Displays the local state snapshot
- `terraform destroy`
	- Destroys the remote infrastructure/objects managed by Terraform
## Importing to Terraform State
To do this, we need to declare a blank _resource_type_ and _resource_name_ to import the infrastructure into.
```
terraform import resource_type.resource_name resource_id
```
This updates the local state and not the configuration file
	- .tf file will need to be manually updated
![[CS302/images/wk12_terraform_import_01.png]]
![[wk12_terraform_import_01 1.png]]