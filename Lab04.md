### 1.Install docker Desktop:

Windows: 
Open terminal, and run: wsl --install
Download Docker Desktop and install it.
You have to register it before use.

<img width="1670" height="414" alt="image" src="https://github.com/user-attachments/assets/c693c4d2-c6fc-4414-be75-0a9c637af128" />


### Install gitea using docker on your computer.

https://about.gitea.com/ 	  
https://docs.gitea.com/installation/install-with-docker

#### a. Does it support LFS? prove it.
**Git LFS is a tool that enables Git to intelligently handle large files. It solves the problem of managing large files in version control systems by replacing "entities" with "pointers", keeping repositories efficient and lightweight.**
<img width="1525" height="548" alt="image" src="https://github.com/user-attachments/assets/ee322a7a-3c2c-4998-821c-e35716a8f893" />
This terminal screenshot provides definitive proof that our Gitea instance supports Git LFS. The successful execution of `git lfs track "*.bin"`and the subsequent generation of the `.gitattributes`file with the correct LFS filter rules (`filter=lfs`) demonstrates that the Gitea server fully accepts and is configured to work with the Git LFS protocol. This is the foundational step required to manage large files with LFS.


#### b. Create a repo with a large file (1G+)

<img width="1647" height="1483" alt="image" src="https://github.com/user-attachments/assets/6ddc5b19-e9f3-4ad9-8c27-f28a916ac641" />

In the push output log, you can see this critical line:  

Downloading LFS objects: 100% (1/1), 1.1 GB | 30 MB/s, done  

**This log entry is the most direct evidence, proving that:**

1. **The Gitea server fully supports LFS** (it is actively processing LFS objects).
2. **I successfully pushed a large file of 1.1 GB**.


#### c. Create a repo for this module and commit your work to this repo.
<img width="1837" height="742" alt="image" src="https://github.com/user-attachments/assets/9a9fa8dc-5171-4e22-833d-f209af56dab0" />
I have created a repository named 'devops-lab4' on Gitea and successfully pushed the lab04 job
