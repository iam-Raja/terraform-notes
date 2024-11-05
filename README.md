# terraform-notes

### What is terraform  :
* Terraform is an open-source infrastructure as code (IaC) tool developed by HashiCorp. It enables us to define and manage infrastructure resources such as virtual machines, networking components, and storage entities across various cloud providers like AWS, Azure, Google Cloud Platform, and others. With Terraform, you describe your desired infrastructure in configuration files (often written in HashiCorp Configuration Language, or HCL), and Terraform handles the provisioning and management of those resources.

### Terraform advantages :
1. Open source:It is a open source, it supports hybrid cloud. We depoly infra across various cloud platfroms.
2. Reuse: We can reuse the configuration. Using the same configuration for an infrastructure we can create multiple environments.
3. Cost: Creation and deletion of takes less time. so when ever Infra not required we delete when required we can create it in less time.
4. Dependicies: Dependicies would resolved automatically while CRUD.
5. State management:Users can easily roll back to the previous configuration. Because, all the configurations in terraform are version controlled and the state is managed.
6. Versions:Since it is a code we can maintain different version of our code

### Terraform Commands :
1. terraform init: Initializes your Terraform configuration directory. It prepares the environment by downloading necessary plugins and modules defined in your configuration files.
2. terraform plan: Provides the Blueprint on your Terraform configuration files. It shows you what actions Terraform will take when you apply your configuration (e.g., create, update, delte resources).
3. terraform apply: Resources will be created or updated according to our Terraform configuration files.
4. terraform destroy: Destroys all resources managed by Terraform in your current configuration. It removes everything that Terraform previously created, helping you to clean up resources when they are no longer needed.
5. terraform validate: Checks the syntax and validity of your Terraform configuration files. It ensures that your configurations are correctly formatted and free of basic errors before applying them.
6. terraform output: Displays the output values defined in your Terraform configuration files. These outputs can include important information about your infrastructure resources, such as IP addresses, URLs, or configuration details.
7. terraform fmt: Formats your Terraform configuration files to ensure consistent style and readability. It automatically adjusts indentation, spacing, and structure according to Terraform's conventions, making your code easier to understand and maintain.

### state in terraform :
* Terraform state file is a JSON file that stores information about the infrastructure resources managed by Terraform. It keeps track of the current state of the infrastructure, including the resources created, their attributes, and their relationships.
The state file is used by Terraform to:
1. Store the current state of the infrastructure
2. Track changes made to the infrastructure
3. Plan and apply changes to the infrastructure
4. Manage dependencies between resources
The state file is typically named "terraform.tfstate" and is stored in the working directory where Terraform is run.

### Remote-state in terraform :
* Saving state file locally is not recommended in terrafrom.Because in a collebrative environment multiple persons working on the smae infra, so there is a high possibility of duplication and errors if we save state locally.
Terraform recommends storing the state file in centralised location, accessible by the entire team and it should be locked so that multiple persons can't do the changes in infrastructure at a time.
S3 can be used to store the statefile and locking with dynamodb

### Variables :
* Variables are used to parameterize the infrastructure. we can provide dynamic values to the configuration through variables

### Locals :
* locals are like variables in some aspects. we can set keys, values and use it whenever we want.It has an extra capabilities it can hold expressions and functions to locals and refer whenever we required.variables can be overriden through to tf vars and cli,but locals cna't be overridden.Variables can be used inside the locals but locals can't be used inside the variables

### Datasource :
* we can query the information from the cloud using the data sources.We can retrive the existing resources details and use them while creating the inra

### Output :
* In Terraform, outputs allow you to expose information about your infrastructure. These output values are useful while creating other resources.
Module developers expose the output values, module users can catch and use them to create the other resources

### Tfvars :
* Tfvars is the file which has key, value pairs.it is used to supply the values to terraform variables.If a default value is specified in a variable file Tfvars can override those values.
we can use different Tfvars files like dev.tfvars and prod.tfvars to provision the infrastructure in multiple environments.
we should use -var-file tag to pass tfvar file to the terraform command.
terraform apply -var-file=dev.tfvars

### What are functions and name few functions:
* Fuctions are to do a unit of work, it can accept inputs and provide the output for us.
Split:Split function to split the values based on the separator.
Slice:slice function to get a part from a list.
Join:join function that helps you mix elements from a list into a single string
Element:Element function is to find out a particular index element.
Length:Length function is to know the size of a list.
Merge:Mergeing

### Workspace in terraform :
* Workspaces in Terraform are isolated environments that allow you to manage multiple, separate infrastructure configurations within a single Terraform working directory. Each workspace contains its own state file and configuration, allowing you to manage different environments, regions, or applications without conflicts.
advantages:Less code
disadvantages:While dealing the variables and their values we should be very careful.
*With the workspaces we can create the multiple environments

###  Provisioners in terraform :
* Provisioners are used to execute scripts or commands on a local or remote machine as part of resource creation or destruction.
Provisioners Will run only when the resources are creating.
Provisioners are 3 types:
1. loca-exec: Executes commands on the machine running Terraform, typically used for local actions like initializing a database or installing software.
2. Remote-exec: Executes commands on a remote machine over SSH or WinRM, typically used to bootstrap or configure resources after they are provisioned.
For this we need connection block.
3. File-exec: Copies files or directories from the machine running Terraform to the newly created resource, useful for transferring configuration files or script

### Module in terraform :
* In terraform, modules are continers for organzing and reusing the terraform configuration.They allow us to package a set of configuration and resources into a reusable component, making it easier to mange and maintain infrastructure code

### Manage secrets and sensitive data in Terraform :
* Managing secrets and sensitive data in Terraform require careful consideration to ensure security. Best practices include:
- Never Hardcode secrets in your Terraform code
- Storing secrets outside of version-controlled files, using tools like HashiCorp Vault or cloud-specific secret management services.
- Utilizing Terraform input variables or environment variables to pass sensitive values securely during runtime.
By following these practices, you can protect sensitive information and minimize the risk of exposing secrets unintentionally

### Terraform best practises :
* - Never Hardcode secrets in your Terraform code
- Do not repeat resourcetype in resourcename
- Resources,variables,outputs these are releated to terraform we can use (_) to separate words.
- User names can have (-) to separate words.
- tagging startegy
- use name main.tf if it is only one resource

### :
*