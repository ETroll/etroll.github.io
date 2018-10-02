---
title: "Creating a Azure Virtual Machine from an existing managed disk"
author: "Karl Syvert Løland"
layout: "blogpost"
tags:
- AZURE
- CLI
- VIRTUAL MACHINE
---

We had created a VM in a Vnet that we was migrating away from. So we were looking for a way to change the connected VNet for a VM in Azure.
Unfortiunatly we could not find any method. And we had to delete the VM and create a new VM from the existing OS disk. This was luckily a
very straight forward process and easy. We also wanted to use a fixed IP and created a NIC with a fixed IP to use. But to use this NIC on the
newly created VM we had to attaach it "manually" via CLI and remove the previous NIC.

* Do steps in portal (se images)
* Attach data disk (if needed)
* Attach NIC if needed
    - Stop VM
    - Do script (Azure CLI example)

```
az vm deallocate --resource-group myResourceGroup --name myVM
az vm nic add --resource-group NE-Infrastructure-Rg --vm-name NE-Build01 --nics NE-Build01-NIC
az vm nic remove --resource-group NE-Infrastructure-Rg --vm-name NE-Build01 --nics ne-build01124
az vm start --resource-group myResourceGroup --name myVM
```
