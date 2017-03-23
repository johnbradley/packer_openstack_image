# packer_openstack_image
Create image in private openstack cloud via packer

packer can create an image in your openstack cloud with this process:
- launch a temporary(builder) VM
- ssh into the vm and add software
- creating an openstack image in your cloud
- deleting the temporary VM


## Setup
- Install packer: https://www.packer.io/docs/installation.html
- Setup openstack environment variables (OS_PROJECT_ID, OS_PROJECT_NAME, OS_PASSWORD). I did this by downloading the Openstack RC file v3. I had to manually set OS_DOMAIN_NAME.
```
source <tenant>-openrc.sh
export OS_DOMAIN_NAME=Default
```
## Gather names and IDs specific to your openstack cluster
- source_image - this is the id of the image that will be your builder
- flavor - this is the flavor that will be used in your builder
- security_groups - security groups used in the builder (will need to include ssh security)
- networks - you will need the ID of a public facing network(so packer can ssh)

Then edit __ubuntu.json__ filling in your cluster specific values

## Create your image
```
packer build ubuntu.json
```


