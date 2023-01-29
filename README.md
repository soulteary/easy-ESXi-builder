# Easy ESXi Builder

Still having trouble building environments for ESXi? Just use this one-click tool.

## Usage

Get Builder Tools:

```bash
docker pull soulteary/easy-esxi-builder:2023.01.29
```

Download ESXi Offline Bundle (eg: `VMware-ESXi-8.0-20513097-depot.zip`) and the community drivers or applications as you need, put them at the same directory, run:

```bash
docker run --rm -it -v `pwd`:/data soulteary/easy-esxi-builder:2023.01.29
```

Enter the docker build env, and build the ESXi image as the same:

```bash
# eg, add base image
Add-EsxSoftwareDepot /data/VMware-ESXi-8.0-20513097-depot.zip

# eg, add community NVMe driver
Add-EsxSoftwareDepot /data/nvme-community-driver_1.0.1.0-3vmw.700.1.0.15843807-component-18902434.zip

# eg, add community PCIe driver
Add-EsxSoftwareDepot /data/Net-Community-Driver_1.2.7.0-1vmw.700.1.0.15843807_19480755.zip

# eg, add community USB driver
Add-EsxSoftwareDepot /data/ESXi800-VMKUSB-NIC-FLING-61054763-component-20826251.zip

# etc ...

# get the image profile, create new profile

Get-EsxImageProfile
New-EsxImageProfile -CloneProfile "ESXi-8.0.0-20513097-standard" -name "ESXi-8.0.0-20513097-standard-nic" -vendor "soulteary"

# get the community drivers, and add them to new profile

Get-EsxSoftwarePackage 

Add-EsxSoftwarePackage -ImageProfile "ESXi-8.0.0-20513097-standard-nic" -SoftwarePackage "nvme-community"
Add-EsxSoftwarePackage -ImageProfile "ESXi-8.0.0-20513097-standard-nic" -SoftwarePackage "net-community"
Add-EsxSoftwarePackage -ImageProfile "ESXi-8.0.0-20513097-standard-nic" -SoftwarePackage "vmkusb-nic-fling"

# make new installer, save iso to `/data`

Export-EsxImageProfile -ImageProfile "ESXi-8.0.0-20513097-standard-nic" -ExportToIso -FilePath /data/ESXi8.iso
```

Full Guide Here (maybe need translate): https://soulteary.com/2023/01/29/how-to-easily-create-and-install-a-custom-esxi-image.html
