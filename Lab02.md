# Lab 02: Nebula VPN Configuration and Connectivity

## 1. Cryptographic Assets Received 

The security and identity of the node rely on three essential files provided by the lecturer (Certificate Authority).

| File Name | Role & Type | Core Function in Nebula | Security Requirement |
| :--- | :--- | :--- | :--- |
| **`yinyuang.crt`** | **Client Certificate** (Public Key) | **Proves your identity** to the network peers and Lighthouse. It contains the public key necessary for others to encrypt data for you. | Publicly shareable (but used internally for identity). |
| **`yinyuang.key`** | **Private Key** | Used to **decrypt data** sent to your node and to create **digital signatures** to authenticate your outgoing messages. | **MUST be kept absolutely confidential.** |
| **`ca.crt`** | **Root CA Certificate** | Establishes the network's **trust domain**. It verifies that your `yourname.crt` (and all other peer certificates) were issued by the trusted CA. | Publicly shareable, needed by all nodes. |
<img width="1495" height="671" alt="image" src="https://github.com/user-attachments/assets/9239c504-44d2-4d34-a158-cfcf89af8bae" />

## 2. Configuration and Deployment 

### Step 2: Customizing the Configuration File

A YAML configuration file must be created or modified to define the node's role, IP address, and point to the cryptographic assets.

**Key Configuration Parameters:**

| Section | Parameter | Customization |
| :--- | :--- | :--- |
| `pki` | `cert` | Path to your **`yourname.crt`** |
| `pki` | `key` | Path to your **`yinyuang.key`** |
| `pki` | `ca` | Path to the root **`ca.crt`** |
| `static_host_map` | `192.168.100.1` | The Lighthouse's public IP/port for initial contact. |
| `firewall` | `inbound`/`outbound` | Custom rules to allow traffic (e.g., ICMP/Ping, SSH). |

<img width="924" height="143" alt="image" src="https://github.com/user-attachments/assets/03c37a07-01f1-494c-8028-85e18e74b280" />

### Step 3: Running the Nebula Daemon
<img width="1638" height="355" alt="image" src="https://github.com/user-attachments/assets/b99865b4-2cea-49f4-b8c6-b8ec08a1feee" />

## 3. Connectivity Verification (连通性验证)
### Step 4: Testing ICMP Connectivity (Ping Test)
From a separate terminal window, the connectivity to the Lighthouse (IP 192.168.100.1) is tested using the ICMP protocol (Ping).
ping 192.168.100.1
<img width="1586" height="674" alt="image" src="https://github.com/user-attachments/assets/4c506c6d-832c-4373-850a-d74f3b46ff26" />

### Step 5: Testing Application Layer Connectivity (SSH Login)
To confirm that the secure tunnel can reliably pass application traffic and that the identity is fully verified, an SSH login attempt is made.

<img width="1621" height="695" alt="image" src="https://github.com/user-attachments/assets/63e9bde7-df61-45e6-8647-243cedc7760f" />



