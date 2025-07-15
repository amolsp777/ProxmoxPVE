# Getting Started with Proxmox VE

## System Requirements

### Hardware Requirements
- Minimum: 2 CPU cores, 8GB RAM, 30GB storage
- Recommended: 4+ CPU cores, 16GB+ RAM, 100GB+ storage
- Network: 2x Gigabit Ethernet ports
- Storage: SSD recommended for system disk

### Software Requirements
- 64-bit CPU with hardware virtualization (Intel VT-x or AMD-V)
- BIOS/UEFI with virtualization enabled
- Minimum 2TB storage for VMs/containers

## Installation Guide

### Step 1: Prepare Installation Media
1. Download Proxmox VE ISO from official website
2. Create bootable USB drive using Rufus or similar tool

### Step 2: Hardware Preparation
```plaintext
BIOS/UEFI Settings:
- Enable VT-x/AMD-V
- Enable VT-d/IOMMU
- Disable Secure Boot
- Set boot order to USB first
```

### Step 3: Installation Process
1. Boot from USB drive
2. Select language and keyboard layout
3. Configure network (DHCP or static)
4. Set root password
5. Configure hostname and domain
6. Select disk for installation
7. Complete installation

## Initial Setup

### Post-Installation Configuration
1. Connect to web interface (https://your-server-ip:8006)
2. Login with root credentials
3. Configure network interfaces
4. Set up storage pools
5. Update system packages

### Basic Commands
```bash
# Update system
pveupgrade

# Check system status
pvesh get nodes/localhost/status

# List storage pools
pvesm status

# List network interfaces
ip addr show
```

## Next Steps

Once the initial setup is complete, proceed to:
1. Configure storage pools
2. Set up network interfaces
3. Create your first virtual machine or container
4. Configure backup system

## Troubleshooting

### Common Issues
- **Virtualization not enabled**: Check BIOS settings
- **Network connectivity**: Verify cable connections and switch ports
- **Storage issues**: Check disk health and permissions
- **Web interface access**: Ensure ports 8006 and 443 are open

## References
- [Proxmox VE Official Documentation](https://pve.proxmox.com/wiki/Main_Page)
- [Proxmox VE Community Forum](https://forum.proxmox.com/)
