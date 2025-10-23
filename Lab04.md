# Lab 04: Docker, Gitea Deployment, and Git LFS Verification
This lab involved setting up the Docker environment, deploying a self-hosted Git service (Gitea) using Docker, and confirming its capability to handle large files via Git Large File Storage (LFS).
## 1. Environment Setup

### 1.1 Docker Desktop Installation

The foundational step was preparing the Windows environment for containerization.

1.  **Install WSL:** Open the terminal and run `wsl --install` to ensure the Windows Subsystem for Linux is operational, as Docker Desktop relies on the WSL 2 backend.
2.  **Install and Register Docker Desktop:** Downloaded and installed Docker Desktop, followed by registration and configuration, making the Docker engine available for local development and deployment.

<img width="1670" height="414" alt="image" src="https://github.com/user-attachments/assets/c693c4d2-c6fc-4414-be75-0a9c637af128" />


### 1.2 Deploying Gitea via Docker

Gitea was deployed as a self-hosted Git platform using containerization for ease of setup and management.

*Gitea is an open-source, lightweight Git service that provides core version control functionality similar to GitHub.*

https://about.gitea.com/ 	  

https://docs.gitea.com/installation/install-with-docker

## 2. Git LFS Functionality Verification

Git LFS (Large File Storage) is a critical extension for managing binary assets and large files in Git repositories by replacing large files with pointers.

### 2.1 Does Gitea Support LFS?

**Yes, Gitea fully supports Git LFS.**

The following terminal steps demonstrate the local client configuration for LFS, which is the foundational requirement for LFS interaction with the server.
<img width="1525" height="548" alt="image" src="https://github.com/user-attachments/assets/ee322a7a-3c2c-4998-821c-e35716a8f893" />
The successful execution of `git lfs track "*.bin"` and the subsequent creation of the `.gitattributes` file confirms that the Git client is correctly configured with the LFS filter, preparing the files for server-side LFS processing.

### 2.2 Proof of Large File Handling (1GB+)

To definitively prove Gitea's LFS support, a repository was created, and a large file (exceeding 1 GB) was pushed.


<img width="1647" height="1483" alt="image" src="https://github.com/user-attachments/assets/6ddc5b19-e9f3-4ad9-8c27-f28a916ac641" />
**Definitive Evidence:**
The push output log contains the critical line:
> **`Downloading LFS objects: 100% (1/1), 1.1 GB | 30 MB/s, done`**

**This log entry is the most direct evidence, proving that:**

1. **The Gitea server fully supports LFS** (it is actively processing LFS objects).
2. **I successfully pushed a large file of 1.1 GB**.
This log entry serves as the most direct proof that:
1. The local Git client successfully executed the LFS protocol.
2. The **Gitea server is actively processing and storing the large file (1.1 GB) as an LFS object**, thus confirming robust LFS functionality.

## 3. Repository Creation and Work Commit

### 2.3 Commit Work to a Module Repository

A new repository was created on the self-hosted Gitea instance specifically for this module's work, ensuring centralized version control for lab deliverables.
<img width="1837" height="742" alt="image" src="https://github.com/user-attachments/assets/9a9fa8dc-5171-4e22-833d-f209af56dab0" />
**Action Confirmation:**
A repository named **`devops-lab4`** was successfully created on the Gitea instance, and the relevant lab work was committed and pushed to this new remote repository, confirming the platform is ready for active development use.
