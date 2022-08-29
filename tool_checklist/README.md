## Tool checklist tiếp nhận hạ tầng về vhkt 

#### Features

- Automatically check evaluation parameters during infrastructure reception

### Supported Vendors

| HPE | DELL | FUJITSU |
| --- | ---- | ------- |
| iLO 4 | iDRAC 8 |iRMC S5 |
| iLO 5 | iDRAC 9 | - |  

#### Requirements

- Environment: Python3

- Node deployment must be able to connect to:

  - IP MM (iLO/iDRAC) port 80,443
  - IP OS port 22
  - IP DCIM (10.255.58.203) port 80
  - IP Gitlab repo (10.240.203.2) port 8180

#### Deployment  

- Pull source code, go to the working directory and install requirements

```bash
git clone http://10.240.203.2:8180/cloud-team/cloud-scripts.git
cd cloud-scripts/tool_checklist
pip3 install -r requirement.txt
```

- Create file input excel like the example below. Put it to node deployment then
 run the code

```bash
python3 device_collect.py -i /path/input.xlsx -o /path/output.xlsx
```

- Input example

> http://10.240.203.2:8180/cloud-team/cloud-scripts/-/blob/master/tool_checklist/input.xlsx

| Loại (compute=1, ceph=2, bare-metal=3) | IP MM (Optinal) | User MM | Pass MM | IP OS | Pass vt_admin | Pass root |
| -------------------------------------- | --------------- | ------- | ------- | ----- | ------------- | --------- |
| 1 | 10.60.1.1 | administrator | pass_mm | 10.1.1.1 | password | password |
 
- Output example

> http://10.240.203.2:8180/cloud-team/cloud-scripts/-/blob/master/tool_checklist/output.xlsx

| **Result** | **IP_OS** | **Type** | **Health** | **Hostname** | **CPU** | **RAM** |**Disk** | **Fan** | **Power** | **Network Card** | **SNMP** | **BIOS_Config** | **Serial** | **Firmware** | **Capacity** | **BIOS_Date** | **BIOS_Version** | **OS_Distribution** | **Iptables_Status** | **Number_Iptables_rules** | **Number_Iptables_rules_in_file** | **Bond** | **Bond0** | **Bond1** | **IP_Manager** | **Product_Name** | **Vendor_Name** | **Logical_Volume** | **HBA** | **Define_in_dcim**|**Contract_in_dcim** |**Warranty_in_dcim** | **License_in_dcim** | **Verify_status_in_dcim** | **Monitored_in_dcim** |    
| ------ | ------ | ------| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |  ------ | ------ | ------ | ------ | ------ | ------ | ------ |------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| NOK | 10.1.1.1 | Compute | OK | hlc-vtn-10.1.1.1 | OK. 2xIntel(R) Xeon(R) Gold 6252 CPU @ 2.10GHz | OK. total: 256GB, 4x64GB DDR4 | OK. Logical: RAID 1 - 2x600GB HDD 10K, Physical: 2x600GB HDD 10K | OK. 6 FAN | OK. 2x500W | OK. 2 card(s): HPE Ethernet 10Gb 2-port 562FLR-SFP+ Adpt, HPE Ethernet 1Gb 4-port 331i Adapter - NIC | OK. State: Enabled. String: ['public', 'snmpcommunity', ''] | OK. {'thermal': 'OptimalCooling', 'power_performance': 'StaticHighPerf'} |  SHGNKIU | iLO 5: v2.12 Jan 17 2020. BIOS: U30 v2.34 (04/08/2020) | 96CPUs,257434MB | 04/08/2020 | U30 | 7.8 | OK. iptables.service   enabled | 861 | '908 | OK | 20000,802.3ad,layer3+4,100ms | ,,,ms | 10.60.1.1 | ProLiant DL380 Gen10 | HPE | ['  root centos -wi-ao---- <525.90g  ', '  swap centos -wi-ao----   32.00g '] | OK. ['Online', 'Online'];['16 Gbit', '16 Gbit'] | OK | NOK. {'product_id': UNKNOWN, 'contract_number': UNKNOWN} | OK. {'name': Bảo Hành, 'start_date': 2020-03-23, 'expiration_date': 2023-04-21} | NOK. {'name': UNKNOW, 'start_time': 2021-03-16T07:00:00+07:00, 'end_time': None} | OK. Verified | OK. PROMETHEUS |
