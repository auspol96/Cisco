# VLAN Configuration and Connectivity Testing Manual

## **Objective**
Configure VLANs on a multilayer switch and ensure that devices in the same VLAN can communicate while blocking communication between different VLANs without routing.

---

## **Step 1: Create VLANs**

1. Enter configuration mode:
   ```shell
   Switch# configure terminal
   ```
2. Create VLANs:
   ```shell
   Switch(config)# vlan 1
   Switch(config-vlan)# name VLAN1
   Switch(config-vlan)# exit
   
   Switch(config)# vlan 2
   Switch(config-vlan)# name VLAN2
   Switch(config-vlan)# exit
   
   Switch(config)# vlan 3
   Switch(config-vlan)# name VLAN3
   Switch(config-vlan)# exit
   ```

3. Assign VLANs to interfaces:
   ```shell
   Switch(config)# interface range fastEthernet 0/11 - 12
   Switch(config-if-range)# switchport mode access
   Switch(config-if-range)# switchport access vlan 1
   Switch(config-if-range)# exit
   
   Switch(config)# interface range fastEthernet 0/13 - 14
   Switch(config-if-range)# switchport mode access
   Switch(config-if-range)# switchport access vlan 2
   Switch(config-if-range)# exit
   
   Switch(config)# interface range fastEthernet 0/15 - 16
   Switch(config-if-range)# switchport mode access
   Switch(config-if-range)# switchport access vlan 3
   Switch(config-if-range)# exit
   ```

---

## **Step 2: Verify VLAN Configuration**
1. Check VLAN assignments:
   ```shell
   Switch# show vlan brief
   ```
   Expected output:
   ```shell
   VLAN Name                             Status    Ports
   ---- -------------------------------- --------- -------------------------------
   1    default                          active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
   2    VLAN2                            active    Fa0/13, Fa0/14
   3    VLAN3                            active    Fa0/15, Fa0/16
   ```

---

## **Step 3: Assign IP Addresses to PCs**
Each PC must have an IP address in its respective VLAN.

### **PC0 (VLAN 1):**
- **IP Address:** 192.168.1.2
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** (leave blank for now)

### **PC1 (VLAN 2):**
- **IP Address:** 192.168.2.2
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** (leave blank for now)

### **PC2 (VLAN 3):**
- **IP Address:** 192.168.3.2
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** (leave blank for now)

---

## **Step 4: Connectivity Testing**
### **Same VLAN Communication Test**
1. From **PC0 (VLAN 1)**, ping **PC1 (VLAN 1)**:
   ```shell
   ping 192.168.1.2
   ```
   - ✅ **Success expected** (since both are in the same VLAN).

2. From **PC2 (VLAN 2)**, ping **PC3 (VLAN 2)**:
   ```shell
   ping 192.168.2.3
   ```
   - ✅ **Success expected**.

### **Inter-VLAN Isolation Test**
1. From **PC0 (VLAN 1)**, ping **PC2 (VLAN 2)**:
   ```shell
   ping 192.168.2.2
   ```
   - ❌ **Should fail** (since VLANs are isolated).

2. From **PC1 (VLAN 2)**, ping **PC3 (VLAN 3)**:
   ```shell
   ping 192.168.3.2
   ```
   - ❌ **Should fail**.

---

## **Conclusion**
This manual provides a structured approach to VLAN configuration, IP assignment, and connectivity testing. The setup ensures proper VLAN isolation and communication within VLANs. If inter-VLAN communication is required, additional routing configurations are needed.

✅ **Success! Ready to be uploaded to GitHub for documentation.** 🚀

