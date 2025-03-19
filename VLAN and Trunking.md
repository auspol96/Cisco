# **VLAN and Trunking Configuration Guide**

## **Objective**
This guide will walk students through the process of configuring VLANs, setting up trunk ports, and ensuring inter-switch VLAN communication. Students will verify connectivity and troubleshoot if necessary.

---

## **Step 1: Verify Existing VLANs**
Before making changes, check the current VLAN configuration on **Switch 1 (SW1)**:
```shell
SW1# show vlan brief
```
- Ensure that **VLANs 1, 2, and 3** exist.
- If VLAN 2 and VLAN 3 are missing, proceed to Step 2.

---

## **Step 2: Create VLANs**
1. Enter global configuration mode:
    ```shell
    SW1# configure terminal
    ```
2. Create VLAN 2 and VLAN 3:
    ```shell
    SW1(config)# vlan 2
    SW1(config-vlan)# name red-vlan
    SW1(config-vlan)# exit

    SW1(config)# vlan 3
    SW1(config-vlan)# name blue-vlan
    SW1(config-vlan)# exit
    ```
3. Verify VLAN creation:
    ```shell
    SW1# show vlan brief
    ```
    VLAN 2 and VLAN 3 should now be listed.

---

## **Step 3: Assign VLANs to Interfaces**
1. Assign **VLAN 2** to ports **Fa0/13 and Fa0/14**:
    ```shell
    SW1(config)# interface range fastEthernet 0/13 - 14
    SW1(config-if-range)# switchport mode access
    SW1(config-if-range)# switchport access vlan 2
    SW1(config-if-range)# exit
    ```
2. Assign **VLAN 3** to ports **Fa0/15 and Fa0/16**:
    ```shell
    SW1(config)# interface range fastEthernet 0/15 - 16
    SW1(config-if-range)# switchport mode access
    SW1(config-if-range)# switchport access vlan 3
    SW1(config-if-range)# exit
    ```
3. Verify the VLAN assignments:
    ```shell
    SW1# show vlan brief
    ```
    Ports Fa0/13-14 should be assigned to VLAN 2, and Fa0/15-16 should be assigned to VLAN 3.

---

## **Step 4: Configure Trunk Port**
1. Check current trunk status:
    ```shell
    SW1# show interfaces gigabitEthernet 0/1 switchport
    ```
    If **Administrative Mode** is **dynamic auto**, change it to **trunk** mode:
    ```shell
    SW1(config)# interface gigabitEthernet 0/1
    SW1(config-if)# switchport trunk encapsulation dot1q
    SW1(config-if)# switchport mode trunk
    SW1(config-if)# switchport trunk allowed vlan 1,2,3
    SW1(config-if)# exit
    ```
2. Verify trunk settings:
    ```shell
    SW1# show interfaces trunk
    ```
    Ensure VLANs 1, 2, and 3 are **allowed and active** on the trunk.

---

## **Step 5: Configure Second Switch (SW2)**
1. Ensure VLAN 3 exists on **SW2**:
    ```shell
    SW2# show vlan brief
    ```
    If VLAN 3 is missing, create it:
    ```shell
    SW2(config)# vlan 3
    SW2(config-vlan)# name blue-vlan
    SW2(config-vlan)# exit
    ```
2. Assign **VLAN 3** to ports **Fa0/23 and Fa0/24**:
    ```shell
    SW2(config)# interface range fastEthernet 0/23 - 24
    SW2(config-if-range)# switchport mode access
    SW2(config-if-range)# switchport access vlan 3
    SW2(config-if-range)# exit
    ```
3. Configure trunk port **Gig0/2** to connect with **SW1**:
    ```shell
    SW2(config)# interface gigabitEthernet 0/2
    SW2(config-if)# switchport trunk encapsulation dot1q
    SW2(config-if)# switchport mode trunk
    SW2(config-if)# switchport trunk allowed vlan 1,2,3
    SW2(config-if)# exit
    ```
4. Verify trunking:
    ```shell
    SW2# show interfaces trunk
    ```
    Ensure VLANs 1, 2, and 3 are listed.

---

## **Step 6: Test Connectivity**
### **Same VLAN Communication Test**
1. **Ping between PCs in the same VLAN:**
    - Example: **PC2 (VLAN 1)** → **PC6 (VLAN 1)**
    ```shell
    PC2> ping 192.168.0.X
    ```
    ✅ Expected: **Successful ping.**

    - Example: **PC4 (VLAN 3)** → **PC8 (VLAN 3)**
    ```shell
    PC4> ping 192.168.2.X
    ```
    ✅ Expected: **Successful ping.**

---

### **Inter-VLAN Connectivity (Negative Test)**
2. **Ping between different VLANs (should fail):**
    - Example: **PC0 (VLAN 1)** → **PC4 (VLAN 3)**
    ```shell
    PC0> ping 192.168.2.X
    ```
    ❌ Expected: **Ping fails** (No routing between VLANs).

---

## **Conclusion**
This guide walks through the process of:
✅ Creating VLANs  
✅ Assigning VLANs to ports  
✅ Configuring trunking between switches  
✅ Testing VLAN communication  

Students should now have a fully operational VLAN setup with proper isolation between VLANs unless routing is enabled.

🚀 **Upload this documentation to GitHub for reference!**

