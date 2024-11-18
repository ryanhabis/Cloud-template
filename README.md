# Virtual Machines Setup (Windows & Linux)

This repository contains Azure Resource Manager (ARM) templates and parameter files to deploy a Windows and a Linux Virtual Machine (VM) in an Azure environment. The configurations cover aspects like networking, IP addressing, and security rules for both VMs.

## Files

- **template.json**: ARM template for deploying the VMs and associated resources.
- **parameters.json**: Parameter file to customize specific values in the template.

## Resources

### Virtual Machines
- **Linux VM**: Configured with Ubuntu 24.04 LTS.
  - OS Disk Size: 30 GB
  - VM Size: Standard_B1s
  - IP Address: Configured as static with regional tier.
  
- **Windows VM**: Configured with Windows Server 2022 Datacenter.
  - OS Disk Size: 127 GB
  - VM Size: Standard_B2s
  - IP Address: Configured as static with regional tier.

### Networking
- **Virtual Network**: `lab-vnet` with address space `10.0.0.0/16`.
- **Subnet**: `lab-subnet-1` with address prefix `10.0.0.0/24`.

### Network Security Groups (NSGs)
Each VM is associated with a dedicated NSG to control inbound access.

- **Linux VM NSG**:
  - Allow SSH on port 22.

- **Windows VM NSG**:
  - Allow RDP on port 3389.
  - Allow SSH on port 22.

## Deployment

To deploy these resources, use the following command in Azure CLI:

```bash
az deployment group create --resource-group <your-resource-group> --template-file template.json --parameters @parameters.json
```

Replace `<your-resource-group>` with your Azure Resource Group name.

## Notes
- Ensure SSH keys are configured if accessing the Linux VM remotely.
- Verify the inbound rules for both NSGs to align with your security policies.
