### README: VLAN Configuration using VLAN Trunking Protocol (VTP)

#### Overview
This project implements VLAN segmentation using **VLAN Trunking Protocol (VTP)** to centrally manage VLAN configurations across a network. The setup involves a **VTP Server** and multiple **VTP Clients** to ensure efficient and consistent VLAN propagation.

---

#### Objectives
1. Configure VLANs on the VTP server and propagate them to client switches.
2. Set up the **VTP domain** and secure it with a password.
3. Ensure trunk links are configured for VLAN communication across the network.
4. Assign VLAN names and confirm synchronization on all switches.

---

#### Steps for Configuration

1. **VTP Server Configuration**
   - Switch S5 is configured as the **VTP Server**, responsible for creating and propagating VLAN configurations.
   - The **VTP domain** is set to `Cyber` with the password `cyber`.
   ```plaintext
   S5(config)# vtp mode server
   S5(config)# vtp domain Cyber
   S5(config)# vtp password cyber
   ```

2. **VLAN Creation on the Server**
   - VLANs are created on the server, and names are assigned for clarity:
     - **VLAN 10**: Name `HR` (Human Resources)
     - **VLAN 20**: Name `Finance`
     - **VLAN 30**: Name `Legal`
   ```plaintext
   S5(config)# vlan 10
   S5(config-vlan)# name HR
   S5(config)# vlan 20
   S5(config-vlan)# name Finance
   S5(config)# vlan 30
   S5(config-vlan)# name Legal
   ```

3. **VTP Client Configuration**
   - The remaining switches are configured as **VTP Clients**. They receive VLAN configurations from the server:
   ```plaintext
   S1(config)# vtp mode client
   S1(config)# vtp password cyber

   S2(config)# vtp mode client
   S2(config)# vtp password cyber

   S3(config)# vtp mode client
   S3(config)# vtp password cyber

   S6(config)# vtp mode client
   S6(config)# vtp password cyber
   ```

4. **Trunk Ports Configuration**
   - Trunk ports are configured on all switches to allow VLAN tagging and communication between switches:
  
   S5(config)#interface range GigabitEthernet 0/1-2
   S5(config-if-range)#switchport mode trunk
   ```

5. **PC IP Address Configuration**
   - PCs are assigned static IP addresses based on their VLAN subnet. Example:
     - **VLAN 10 (Human Resources)**: `192.168.10.0/24`
     - **VLAN 20 (Finance)**: `192.168.20.0/24`
     - **VLAN 30 (Legal)**: `192.168.30.0/24`
   - Configuration Path: **Desktop > IP Configuration** on each PC.

6. **Verification**
   - Verify VLAN propagation using the `show vlan brief` and `show vtp status` commands on client switches. Confirm that all VLANs created on the server are visible.

7. **Save Configuration**
   - Save the file as `STP exercise with VTP.pkt` for future reference.

---

#### Key Features of the Configuration
1. **Centralized VLAN Management:** VLANs are created and named on the VTP Server (S5) and propagated to all client switches automatically.
2. **Secure Domain:** The VTP domain `Cyber` is protected with a password to prevent unauthorized changes.
3. **Efficient Trunking:** Trunk ports ensure smooth VLAN communication between switches, maintaining a unified network.

---

#### VLAN-to-Switch Mapping
- **VLAN 10 (HR, 192.168.10.0/24):**
  - All PCs in the HR department
- **VLAN 20 (Finance, 192.168.20.0/24):**
  - All PCs in the Finance department
- **VLAN 30 (Legal, 192.168.30.0/24):**
  - All PCs in the Legal department

---

This configuration demonstrates the power of VTP for efficient and scalable VLAN management in a multi-switch network. By automating VLAN propagation, administrative overhead is minimized, and network consistency is ensured.
