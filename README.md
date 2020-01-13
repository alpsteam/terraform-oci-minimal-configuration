# Terraform on Oracle Cloud (Minimal configuration)

This code provides an example of how to use Terraform with Oracle Cloud (minimal config, no resources are provisioned).

### 1) Install Terraform CLI

**Linux/Mac:**

Download the appropriate package for your system from the [Terraform downloads page](https://www.terraform.io/downloads.html). Unzip the package and move it to `/usr/local/bin/`. 

Example:

```
wget https://releases.hashicorp.com/terraform/0.12.19/terraform_0.12.19_linux_amd64.zip
unzip terraform_0.12.19_linux_amd64.zip
mv terraform_0.12.19_linux_amd64/terraform /usr/local/bin
```

Verify the Terraform installation with `terraform version`.

