# Answer Key: Subnet Mismatch and ARP Failure in Cisco Packet Tracer

## 1. Aim

To simulate a subnet mismatch between two PCs in Cisco Packet Tracer and troubleshoot network connectivity by observing ARP resolution failure and ICMP ping results in Simulation Mode.

## 2. Software Required

- Cisco Packet Tracer
- Two PCs (PC0 and PC1)
- One Cisco 2960 switch
- Copper Straight-Through cables

## 3. Initial Network Configuration

| Device | IP Address    | Subnet Mask   |
| ------ | ------------- | ------------- |
| PC0    | 192.168.10.10 | 255.255.255.0 |
| PC1    | 192.168.20.20 | 255.255.255.0 |

Both PCs are connected to the same switch but belong to different IP subnets.

## 4. Step-by-Step Procedure

### Step 1: Create the Network Topology

1. Open Cisco Packet Tracer.
2. Place PC0, PC1, and one 2960 switch in the workspace.
3. Connect both PCs to the switch using Copper Straight-Through cables.
4. Wait until the link indicators become green.

Expected Result: Both PCs are physically connected to the switch.

### Step 2: Configure PC0

1. Click PC0.
2. Open Desktop → IP Configuration.
3. Enter the following details:
   - IP Address: `192.168.10.10`
   - Subnet Mask: `255.255.255.0`

### Step 3: Configure PC1

1. Click PC1.
2. Open Desktop → IP Configuration.
3. Enter the following details:
   - IP Address: `192.168.20.20`
   - Subnet Mask: `255.255.255.0`

Expected Result: The PCs have different subnet addresses.

### Step 4: Switch to Simulation Mode

1. Click Simulation at the bottom-right corner.
2. Open the Simulation Panel.
3. Click Edit Filters.
4. Select only ARP (Address Resolution Protocol) and ICMP (Internet Control Message Protocol).
5. Close the filter window.

Expected Result: Only ARP and ICMP packet events are displayed.

### Step 5: Initiate the Ping Command

1. Click PC0.
2. Navigate to Desktop → Command Prompt.
3. Enter the following command:

```
ping 192.168.20.20
```

4. Press Enter.
5. Observe the ping result and packet events.

Expected Result: The ping fails because PC0 and PC1 belong to different subnets and no router or default gateway is configured.

### Step 6: Modify the Subnet Mask to Demonstrate ARP Failure

1. Return to Realtime Mode.
2. Open PC0 → Desktop → IP Configuration.
3. Change PC0's subnet mask to `255.255.0.0`.
4. Keep PC1's IP address and subnet mask unchanged.
5. Return to Simulation Mode.
6. Run the following command again on PC0:

```
ping 192.168.20.20
```

7\. Observe the ARP and ICMP packet events.

Expected Result: PC0 treats PC1 as a local host and attempts to discover PC1's MAC address using ARP.

### Step 7: Analyze the ARP Packet Drop

1. Click Capture/Forward to advance the simulation.
2. Observe the ARP request travelling from PC0 to the switch.
3. Observe the switch forwarding the ARP broadcast towards PC1.
4. Inspect the packet details by clicking the relevant PDU.
5. Open the Inbound PDU Details or In Layers tab, depending on the Packet Tracer version.
6. Examine the ARP request and the packet processing result.

Expected Result: PC1 does not reply to the ARP request because the request is asking for the MAC address of `192.168.20.20`, which is PC1's own IP only if configured as stated. Therefore, PC1 should normally reply.

Important correction: With the stated configuration, PC1 should respond to the ARP request because the target IP address matches PC1's IP address. To demonstrate a genuine ARP failure, use an unreachable target IP or configure PC1 with a different IP address than the one being pinged. A red X alone does not prove that a subnet mismatch caused the drop.

### Step 8: Correct the Network Configuration

1. Return to Realtime Mode.
2. Open PC1 → Desktop → IP Configuration.
3. Change PC1's IP address to `192.168.10.11`.
4. Set its subnet mask to `255.255.255.0`.
5. Ensure PC0's subnet mask is also `255.255.255.0`.

Use this corrected configuration:

| Device | IP Address    | Subnet Mask   |
| ------ | ------------- | ------------- |
| PC0    | 192.168.10.10 | 255.255.255.0 |
| PC1    | 192.168.10.11 | 255.255.255.0 |

### Step 9: Verify Network Connectivity

1. Click PC0 → Desktop → Command Prompt.
2. Enter the following command:

```
ping 192.168.10.11
```

3. Press Enter.
4. Observe the output.
5. <img width="1312" height="1199" alt="image" src="https://github.com/user-attachments/assets/0ebf552f-ddb3-4e0e-a701-142f8147d2de" />


Expected Result:

```
Reply from 192.168.10.11: bytes=32 time<1ms TTL=128
```

Successful replies indicate that communication between PC0 and PC1 is working.

## 5. Testing Results

| Test                       | Expected Result                          |
| -------------------------- | ---------------------------------------- |
| Physical connection        | Links become green                       |
| Initial ping               | Fails due to different subnets           |
| ARP inspection             | ARP request and response can be observed |
| Corrected IP configuration | Both PCs belong to the same subnet       |
| Final ping                 | Successful replies from PC1              |

## 6. Result

The subnet mismatch scenario was studied in Cisco Packet Tracer. ARP and ICMP packet events were examined in Simulation Mode, and connectivity was restored by configuring both PCs with IP addresses belonging to the same subnet.

## 7. Conclusion

This experiment demonstrates the importance of correct IP addressing and subnet masks in LAN communication. Simulation Mode helps analyze ARP resolution and ICMP ping behaviour to troubleshoot network connectivity problems.

## Author

Krishnaveni

Course: B.Tech – Computer Science and Business Systems
##  Project Status

**Completed**
