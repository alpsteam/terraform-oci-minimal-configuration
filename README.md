# Terraform on Oracle Cloud (minimal configuration)

This code provides an example of how to use Terraform with Oracle Cloud. This is a minimal configuration, no resources will be provisioned. The only thing the script will do is list the [availability domains](https://docs.cloud.oracle.com/iaas/Content/GSG/Concepts/concepts.htm) that are available and output the result:

```
# Get a list of Availability Domains
data "oci_identity_availability_domains" "ads" {
  compartment_id = "${var.tenancy_ocid}"
}

# Output the result
output "show-ads" {
  value = "${data.oci_identity_availability_domains.ads.availability_domains}"
}
```

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

**Windows:**

todo

### 2) Set environment variables

For Terraform to work correctly with your Oracle Cloud tenancy you will need to set some environment variables first. Find all necessary environment variables in the [terraform-oci-minimal-configuration/env_vars file](env_vars). You need to replace every `XXXXXXXXXXXXX` with the correct values. Find instructions on how to aquire these values [here](https://docs.cloud.oracle.com/iaas/Content/API/Concepts/apisigningkey.htm#Other). You will need to upload a public key to the Oracle Cloud console in the process.

Finally, run `source env_vars` to set the variables. You can check if your environment variables were set correctly by running `echo $TF_VAR_region` etc.

**Important!** If you created your private key with a password, you will need to specify the password within the `env_vars` file.

### 3) Apply Terraform script

Change directory into the `terraform-oci-minimal-configuration/` folder.
```
cd terraform-oci-minimal-configuration
ls -a
```
You don't yet have the specific Terraform provider for Oracle Cloud. You can easily download the Terraform Provider for Oracle Cloud with `terraform init`
```
terraform init
ls -a
```
Now you are all set. Check if the Terraform provider for Oracle Cloud is working correctly with the code above by running `terraform validate`. 

If all environment variables are set correctly you should also be able to run `terraform plan` and `terraform apply`. An example output might look like this.

```
➜  terraform-oci-minimal-configuration git:(master) ✗ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.

data.oci_identity_availability_domains.ads: Refreshing state...

------------------------------------------------------------------------

No changes. Infrastructure is up-to-date.

This means that Terraform did not detect any differences between your
configuration and real physical resources that exist. As a result, no
actions need to be performed.

```

If you get an error `Service error:NotAuthenticated. The required information to complete authentication was not provided or was incorrect.. ` you need to re-ckeck if: (1) you uploaded your public key correctly, (2) supplied all environment variables correctly, (3) specified a private key password if necessary.

### 4) Next steps

Continue with a more complex Terraform configuration like [this](https://github.com/alpsteam/terraform-oci-simple-webserver).
