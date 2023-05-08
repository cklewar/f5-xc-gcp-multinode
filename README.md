# F5-XC-GCP-MULTINODE

This repository consists of Terraform templates to bring up a F5XC GCP multi node environment.

## Usage

- Clone this repo with: `git clone --recurse-submodules https://github.com/cklewar/f5-xc-gcp-multinode`
- Enter repository directory with: `cd f5-xc-gcp-multinode`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
- Initialize with: `terraform init`
- Apply with: `terraform apply -auto-approve` or destroy with: `terraform destroy -auto-approve`

### Example Output

```bash
module.gcp_multi_node.volterra_gcp_vpc_site.gcp_site: Creating...
module.gcp_multi_node.volterra_gcp_vpc_site.gcp_site: Creation complete after 2s [id=90c2f729-25b1-4ea5-ada8-faa6ece43f94]
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Creating...
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Still creating... [4m0s elapsed]
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Still creating... [4m10s elapsed]
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Still creating... [4m20s elapsed]
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Still creating... [4m30s elapsed]
module.gcp_multi_node.volterra_tf_params_action.gcp_vpc_action: Creation complete after 4m32s [id=e0ff3d07-590a-4770-9c3e-b7f63808fcd3]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.
```

## Multi Node Single NIC new VPC module usage example

````hcl
module "gcp_multi_node_single_nic_new_network_new_subnet" {
  source                            = "./modules/f5xc/site/gcp"
  f5xc_tenant                       = var.f5xc_tenant
  f5xc_api_url                      = var.f5xc_api_url
  f5xc_gcp_cred                     = "ck-gcp-01"
  f5xc_api_token                    = var.f5xc_api_token
  f5xc_namespace                    = var.f5xc_namespace
  f5xc_gcp_region                   = var.f5xc_gcp_region
  f5xc_gcp_site_name                = format("%s-gcp-mn-snic-new-n-new-s-%s", var.project_prefix, var.project_suffix)
  f5xc_gcp_ce_gw_type               = "single_nic"
  f5xc_gcp_zone_names               = var.f5xc_gcp_zone_names
  f5xc_gcp_node_number              = 3
  f5xc_gcp_local_subnet_name        = format("%s-gcp-mn-snic-new-n-new-s-%s", var.project_prefix, var.project_suffix)
  f5xc_gcp_local_network_name       = format("%s-gcp-mn-snic-new-n-new-s-%s", var.project_prefix, var.project_suffix)
  f5xc_gcp_local_primary_ipv4       = "192.168.169.0/24"
  f5xc_gcp_default_ce_os_version    = true
  f5xc_gcp_default_ce_sw_version    = true
  f5xc_gcp_default_blocked_services = true
  ssh_public_key                    = file(var.ssh_public_key_file)
  providers                         = {
    google   = google.default
    volterra = volterra.default
  }
}

output "gcp_multi_node_single_nic_new_network_new_subnet" {
  value = module.gcp_multi_node_single_nic_new_network_new_subnet.gcp_vpc
}
````

## Multi Node Multi NIC module usage example

````hcl

````