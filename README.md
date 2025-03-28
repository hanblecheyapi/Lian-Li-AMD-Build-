
# 🧰 Custom PC Build & Lab Setup Tracker

---

## ✅ Section 1: Hardware Build Checklist

### 📦 Core Components
- [ ] Lian Li O11 Dynamic EVO XL Case  
- [ ] Asus ROG STRIX X670E-A GAMING WIFI ATX AM5 Motherboard  
- [ ] AMD Ryzen 9 7950X 16-Core CPU  
- [ ] Lian Li Galahad II LCD SL-INF AIO Cooler  
- [ ] Kingston FURY Beast RGB 64GB (2x32GB DDR5-6000)  
- [ ] Samsung 990 Pro 1TB NVMe SSD (Windows)  
- [ ] Corsair MP700 PRO 1TB NVMe SSD (Proxmox)  
- [ ] Samsung 870 EVO 4TB 2.5" SATA SSD (VM Storage)  
- [ ] Lian Li EDGE 1000W 80+ Platinum PSU  
- [ ] 6x Lian Li Uni Fan SL-Infinity 140mm Fans  

### 🔌 Cables & Mounting
- [ ] PSU Cables (modular: SATA, GPU, EPS, etc.)  
- [ ] SATA Data Cable for Samsung 870 EVO  
- [ ] AIO Screws + Backplate  
- [ ] Fan Hub/Controller (if needed for SL-Infinity fans)

### 🛠️ Assembly Tasks
- [ ] Install CPU and apply thermal paste  
- [ ] Install RAM  
- [ ] Mount AIO cooler + fans  
- [ ] Install NVMe SSDs (in correct slots)  
- [ ] Mount 2.5" SSD behind motherboard or lower chamber  
- [ ] Connect PSU and cables  
- [ ] Plug in fans and set up fan hub/controller  
- [ ] Manage cables and route behind tray  
- [ ] First boot into BIOS

---

## 💾 Section 2: Software Install & Boot Plan

### 🖥️ OS & Virtualization Strategy
| Drive | OS / Purpose | Notes |
|-------|--------------|-------|
| Samsung 990 Pro | Windows Server | Gaming / productivity |
| Corsair MP700 PRO | Proxmox VE | Host system for VMs |
| Samsung 870 EVO | VM storage | ISOs, backups, CTFLabs |

### 🧪 Installation Tasks
- [ ] BIOS Settings:
  - [ ] Enable SVM
  - [ ] Enable IOMMU
  - [ ] Enable Above 4G Decoding + Re-size BAR
  - [ ] Set Boot Priority
- [ ] Install Windows Server on 990 Pro
- [ ] Install Proxmox VE on MP700 PRO (manual disk setup)
- [ ] Format 870 EVO for ext4 or ZFS, mount in `/mnt/ssd4tb`
- [ ] Add 870 EVO to Proxmox via GUI

---

## 🎮 Section 3: GPU Passthrough Setup

### VFIO Setup for AMD GPU
- [ ] Edit GRUB: `amd_iommu=on iommu=pt`
- [ ] Update GRUB & Reboot
- [ ] Check IOMMU groups
- [ ] Bind GPU IDs to VFIO
- [ ] Blacklist AMD drivers
- [ ] Update initramfs & reboot
- [ ] Verify isolation (`dmesg`, `lspci`)
- [ ] Create Windows VM with OVMF + PCIe passthrough
- [ ] Install GPU drivers inside VM
- [ ] Optional: passthrough USB devices (mouse/keyboard)

---

## 📓 Section 4: Lab Journal Template

| Date | Task | Result | Notes |
|------|------|--------|-------|
| Mar 27 | Installed Proxmox | Successful | Mounted MP700 PRO as root disk |
| Mar 28 | Enabled IOMMU | ✅ | Ready for GPU passthrough |
| Mar 29 | Windows VM + passthrough | TBD | Need to add USB controller passthrough |

---

## 🔐 Optional Add-Ons (Advanced)

- [ ] Enable PCIe NVMe passthrough for direct VM disk
- [ ] Set up ZFS on 870 EVO for compression/snapshots
- [ ] Install Zeek, Suricata, ELK stack for traffic analysis
- [ ] Add Sunshine/Moonlight for streaming VM to other devices
- [ ] Automate VM deploys with Ansible or cloud-init
