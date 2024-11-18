# Virtual Machines Setup (Windows & Linux) - Updated Version

This repository contains Azure Resource Manager (ARM) templates and parameter files to deploy a Windows and a Linux Virtual Machine (VM) in an Azure environment. The updated templates include specifications for virtual networks, public IPs, and advanced network security rules for each VM.

## Files

- **template.json**: ARM template defining the infrastructure for deploying both VMs, including security groups, public IP addresses, and virtual network configurations.
- **parameters.json**: Parameter file for customizing specific resource names and values within the template.

## Resources

### Virtual Machines

- **Linux VM**
  - OS: Ubuntu 24.04 LTS
  - OS Disk Size: 30 GB
  - VM Size: Standard_B1s
  - Public IP: `172.205.236.95`
  - Security: SSH access via NSG `linux-vm-nsg` on port 22

- **Windows VM**
  - OS: Windows Server 2022 Datacenter
  - OS Disk Size: 127 GB
  - VM Size: Standard_B2s
  - Public IP: `20.93.131.144`
  - Security: RDP and SSH access via NSG `window-vm-nsg` on ports 3389 and 22

### Networking

- **Virtual Network**: `lab-vnet` with address space `10.0.0.0/16`
- **Subnet**: `lab-subnet-1` with address prefix `10.0.0.0/24`
- **Network Security Groups (NSGs)**:
  - **Linux VM**: Allows inbound SSH on port 22.
  - **Windows VM**: Allows inbound RDP on port 3389 and SSH on port 22.

### DDoS Protection and Public IPs

Both VMs have public IP addresses configured with static allocation and DDoS protection set to inherit from the virtual network. The public IP configurations include idle timeouts and address versioning set to IPv4.

## Deployment

To deploy these resources, use the following Azure CLI command:

```bash
az deployment group create --resource-group <your-resource-group> --template-file template.json --parameters @parameters.json
```

Replace `<your-resource-group>` with the appropriate Azure Resource Group name.

## Notes

- Ensure proper SSH keys are configured for secure access to the Linux VM.
- Review and modify NSG rules based on your security requirements before deployment.
- The template includes settings to support trusted launch and secure boot for both VMs.
