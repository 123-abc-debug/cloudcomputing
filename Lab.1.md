## 1. Check if your processor supports Intel/AMD virtualization technology. Enable Intel virtualization technology in BIOS if possible.

**To check support:**
- **Windows**: Open **Task Manager → Performance tab → CPU → Virtualization**  
  - If shown as “Enabled” or “Disabled”, your processor supports virtualization.  
  - If not shown, your processor might not support it.
<img width="987" height="812" alt="image" src="https://github.com/user-attachments/assets/8e7981ec-a820-4450-adfa-c488d872671e" />


**To enable in BIOS:**
1. Restart your computer and press the BIOS key (e.g., **Del, F2, F10, F12**).  
2. Find options like **Advanced → CPU Configuration → Virtualization Technology**.  
3. Set **Intel Virtualization Technology (VT-x)** or **AMD-V** to **Enabled**.  
4. Save and exit (usually **F10**).


## 2.The cloud is almost everywhere in our lives now. What do you think are the fundamental reasons behind its success? Name three pros and three cons of cloud.

### (1) Fundamental reasons for success 
| Reason | Explanation |
| :--- | :--- |
| **Cost Optimization** | Shifts IT spending from high upfront **Capital Expenditure (CapEx)** to flexible **Operating Expenditure (OpEx)**, eliminating costs for hardware procurement and maintenance. |
| **Elasticity & Scalability** | Automatically and quickly adjusts computing resources (storage, processing power) based on real-time demand, preventing resource waste or shortages. |
| **Ubiquitous Access** | Allows users to access data and applications from any device and location via the internet, strongly supporting mobile and remote work scenarios. |
---

### (2) Three pros of cloud 

| Pro | Detail |
| :--- | :--- |
| **Reduced IT Management Burden** | Cloud providers handle infrastructure maintenance, software updates, and security patches, allowing organizations to focus on core business. |
| **Rapid Deployment** | New services or applications can be launched in minutes or hours, significantly accelerating time-to-market compared to traditional on-premises setup (weeks/months). |
| **Disaster Recovery & Backup** | Offers redundant storage and backup solutions across geographically distributed data centers, enhancing data reliability and business continuity. |
---

### (3) Three cons of cloud 

| Con | Risk |
| :--- | :--- |
| **Dependency on Internet** | Cloud services are unavailable if internet connectivity is interrupted or poor, impacting critical business operations. |
| **Security & Privacy Risks** | Data stored on third-party servers may face threats like unauthorized access, data breaches, or compliance issues with regional regulations (e.g., GDPR). |
| **Vendor Lock-in** | Migrating data or applications between different cloud providers can be costly and complex due to incompatible technology stacks, APIs, or service models. |

## 3. What is the primary function of a hypervisor in virtualization?

A **hypervisor (VMM)** creates, manages, and isolates **multiple virtual machines** on one physical host.  
It enables:  
- **Resource allocation** (CPU, memory, storage)  
- **Isolation** between VMs  
- **Hardware abstraction** to run different OSs on one host    

---

## 4. What is a Virtual Machine (VM)? 

A **VM** is a software-based emulation of a physical computer.  
It runs its own **guest operating system** and applications, managed by a **hypervisor** that shares physical resources (CPU, memory, storage, network) among VMs.


## 5️.What are the benefits of using virtual machines?

| Benefit | Explanation |
| :--- | :--- |
| **Resource Efficiency** | Multiple VMs share the host machine's physical hardware, significantly reducing costs for physical servers, power, and data center space (Server Consolidation). |
| **Isolation & Security** | Failures, crashes, or malware in one VM do not spread to other VMs or the host system, enhancing overall system stability and data security. |
| **Flexible Testing & Development** | Developers can quickly create isolated environments with different OS versions or configurations for testing applications without affecting the host system. |
| **Easy Backup & Recovery** | VMs can be saved, cloned, or exported as portable image files, allowing for quick backups and fast restoration to a previous working state. |
| **Legacy Application Support** | Outdated applications or software requiring older operating systems can run securely within a VM, avoiding compatibility issues with modern host OSs. |
---

## 6.List five use cases of virtual machines.
1. **Software Development & Testing:** Utilizing VMs to simulate various operating systems and network environments for comprehensive application testing and debugging.
2. **Server Consolidation:** Reducing the physical server count by running multiple virtual server instances (VMs) on a single physical host, lowering hardware and operational costs.
3. **Education & Training:** Deploying standardized, pre-configured VM environments for students and trainees, ensuring a consistent and safe learning platform.
4. **Cloud Computing Services (IaaS):** Serving as the core technology for Infrastructure-as-a-Service, allowing cloud providers to offer virtualized computing resources (virtual servers) on demand.
5. **Legacy System Migration:** Running outdated or critical business applications that rely on obsolete operating systems within a VM, ensuring business continuity without maintaining old physical hardware.
---

## 7️.In virtualization, what is the guest operating system? 
a) The main operating system running on the physical machine
b) The operating system installed on a virtual machine
c) The operating system running on a remote server
d) The operating system running on a mobile device

> **Answer ：**  
> **b) The operating system installed on a virtual machine**  
A virtual machine is a virtual computer, and the guest operating system is the system you install and use on this virtual computer (for example, if you run a Linux virtual machine on your Windows computer, then Linux is the guest operating system)

---

## 8️.What does virtual machine isolation mean?
a) Virtual machines can communicate directly with the physical hardware.
b) Virtual machines share the same resources and cannot be isolated.
c) Virtual machines run independently and are isolated from each other and the host system.
d) Virtual machines can only be accessed locally.


>  **Answer：**
> **c) Virtual machines run independently and are isolated from each other and the host system.**  

---

## 9. What is the benefit of virtual machine portability?
a) It allows virtual machines to communicate with each other easily.
b) It ensures faster boot times for virtual machines.
c) It allows virtual machines to be moved between different physical machines with compatible hypervisors.
d) It reduces the need for hardware virtualization.

>  **Answer ：**  
> **c) It allows virtual machines to be moved between different physical machines with compatible hypervisors.**  

---

## 10. What is the purpose of cloning a virtual machine?

Cloning creates an **exact, ready-to-use copy** of an existing Virtual Machine (VM), including its operating system, applications, configurations, and data. This avoids the time-consuming process of manually installing and setting up a new VM from scratch.

Common use cases for cloning include:

1.  **Rapid Deployment:** Quickly scaling up services or creating multiple identical environments using a pre-configured template (the original VM).
2.  **Testing and Debugging:** Using clones to test software updates, patches, or new features without risking the stability of the original production VM.
3.  **Disaster Recovery:** Keeping cloned VMs as reliable backups; if the primary VM fails, the clone can be activated immediately to restore services.
4.  **Consistent Environments:** Ensuring all team members (e.g., developers, testers) work on identical, standardized VM environments, eliminating configuration differences.

