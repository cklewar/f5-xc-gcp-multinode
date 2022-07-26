# F5-XC-GCP-MULTINODE

This repository consists of Terraform templates to bring up a F5XC GCP multi node environment.

## Usage

- Clone this repo with: `git clone https://github.com/cklewar/f5-xc-gcp-multinode`
- Enter repository directory with: `cd f5-xc-gcp-multinode`
- Clone __modules__ repository with: `git clone https://github.com/cklewar/f5-xc-modules`
- Rename __modules__ repository directory name with: `mv f5-xc-modules modules`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
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

## Single NIC module usage example

````hcl
module "gcp_multi_node" {
  source                            = "./modules/f5xc/site/gcp"
  f5xc_api_p12_file                 = "/cert/api-creds.p12"
  f5xc_api_url                      = "https://playground.staging.volterra.us/api"
  f5xc_namespace                    = "system"
  f5xc_tenant                       = "playground"
  f5xc_gcp_cred                     = "gcp-01"
  f5xc_gcp_ce_gw_type               = "single_nic"
  f5xc_gcp_default_ce_sw_version    = true
  f5xc_gcp_default_os_version       = true
  f5xc_gcp_inside_primary_ipv4      = "192.168.169.0/24"
  f5xc_gcp_outside_primary_ipv4     = "192.168.168.0/24"
  f5xc_gcp_node_number              = 3
  f5xc_gcp_project_id               = "gcp_project_id"
  f5xc_gcp_region                   = "us-east1"
  f5xc_gcp_site_name                = "gcp-multi-node-01"
  f5xc_gcp_zone_names               = ["us-east1-b"]
  f5xc_gcp_default_blocked_services = true
  public_ssh_key                    = "ssh-rsa xyz"
}
````

## Multi NIC module usage example

````hcl
module "gcp_multi_node" {
  source                            = "./modules/f5xc/site/gcp"
  f5xc_api_p12_file                 = "cert/api-creds.p12"
  f5xc_api_url                      = "https://playground.staging.volterra.us/api"
  f5xc_namespace                    = "system"
  f5xc_tenant                       = "playground"
  f5xc_gcp_cred                     = "gcp-01"
  f5xc_gcp_ce_gw_type               = "multi_nic"
  f5xc_gcp_default_ce_sw_version    = true
  f5xc_gcp_default_os_version       = true
  f5xc_gcp_inside_primary_ipv4      = "192.168.169.0/24"
  f5xc_gcp_outside_primary_ipv4     = "192.168.168.0/24"
  f5xc_gcp_node_number              = 3
  f5xc_gcp_project_id               = "gcp_project_id"
  f5xc_gcp_region                   = "us-east1"
  f5xc_gcp_site_name                = "gcp-multi-node-01"
  f5xc_gcp_zone_names               = ["us-east1-b"]
  f5xc_gcp_default_blocked_services = true
  public_ssh_key                    = "ssh-rsa xyz"
}
````