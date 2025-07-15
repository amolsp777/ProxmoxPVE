# Virtual Machine Management in Proxmox VE

## Creating a New Virtual Machine

### Using Web Interface
1. Click "Create VM" in the web interface
2. Fill in basic settings:
   - VM ID: Automatically assigned
   - Name: Descriptive name
   - OS Type: Linux/Windows
   - Storage: Select pool
   - Memory: Allocate RAM
   - CPU: Select cores
   - Network: Choose interface

### Using Command Line
```bash
# Create a new VM
qm create 100 --name my-vm --memory 4096 --cores 2 --net0 virtio,bridge=vmbr0

# Add disk
qm set 100 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-100-disk-0,format=qcow2,size=20G

# Add ISO
qm set 100 --ide2 local-lvm:vm-100-cloudinit

# Set boot order
qm set 100 --boot c --bootdisk scsi0 --ide2 local-lvm:vm-100-cloudinit
```

## VM Templates

### Creating a Template
1. Install and configure a base VM
2. Shutdown the VM
3. Convert to template:
```bash
qm template 100
```

### Using a Template
```bash
# Clone from template
qm clone 100 101 --name new-vm

# Adjust resources
qm set 101 --memory 2048 --cores 1
```

## Resource Management

### CPU and Memory
```bash
# View current allocation
qm config 100

# Adjust CPU cores
qm set 100 --cores 4

# Adjust memory
qm set 100 --memory 8192
```

### Storage
```bash
# Add new disk
qm set 100 --scsi1 local-lvm:vm-100-disk-1,format=qcow2,size=50G

# Resize existing disk
qm resize 100 scsi0 +10G
```

## Backup and Restore

### Creating Backups
```bash
# Create backup
vzdump 100 --storage backup --compress lzo --mode snapshot

# Schedule backup
vzdump --storage backup --mode snapshot --compress lzo --node proxmox --maxfiles 2 --mailto admin@example.com
```

### Restoring Backups
```bash
# Restore backup
vzdump --restore 100 --file /var/lib/vz/dump/vzdump-qemu-100-2024_01_01-00_00_00.vma.lzo
```

## Monitoring and Maintenance

### Performance Monitoring
```bash
# View VM status
qm status 100

# Monitor CPU usage
qm monitor 100

# Check disk I/O
iostat -x 1
```

### Maintenance Tasks
```bash
# Shutdown VM
qm shutdown 100

# Start VM
qm start 100

# Reboot VM
qm reboot 100

# Delete VM
qm destroy 100
```

## Best Practices

1. Use virtio drivers for better performance
2. Allocate appropriate resources based on workload
3. Regularly backup VMs
4. Use templates for consistent deployments
5. Monitor resource usage and adjust as needed

## Troubleshooting

### Common Issues
- **VM won't start**: Check storage and network connectivity
- **Poor performance**: Verify resource allocation
- **Disk space issues**: Clean up old snapshots and backups
- **Network connectivity**: Verify virtual network configuration

## References
- [Proxmox VE VM Management](https://pve.proxmox.com/wiki/VM_Management)
- [Proxmox VE Storage Management](https://pve.proxmox.com/wiki/Storage)
