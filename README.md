# CS 312 Course Project Part 2
## What will we do?
- Run the GitHub action workflow to create and run an automated Minecraft server.
## How will we do it?
- The solution consists of two files:
  * **The GitHub action workflow:** ```setup-instance.yml```
    * Checks out the repository
    * Creates the EC2 instance
    * Gets the Public IP Address and adds it to the hosts.ini file for Ansible
    * Installs Ansible and nmap
    * Creates the private key
    * Runs the ```install-MC.yml``` Ansible playbook
    * When the playbook is finished, the workflow will connect to the Minecraft server using nmap
  * **The Ansible playbook:** ```install-MC.yml```
    * Downloads and installs Java and Minecraft on EC2
    * Accepts the Minecraft Eula
    * Creates the Minecraft user and service file
    * Installs and starts the Minecraft server

# Requirements
### What will the user need to configure to run the pipeline?
- The user will need to setup the pipeline secrets in order to run the workflow. The user will also need to create a private key in their AWS account called ```MC-Key```. See the **credentials** step below to set up the secrets in GitHub.
### What tools should be installed?
- The script installs Ansible, nmap, Java, and Minecraft.
### Are there any credentials or CLI required?
- The user needs to set up the pipeline secrets and add their AWS credentials to the secrests.
  * To create the secrets on GitHub from the repository homepage:
    * Go to "Settings -> Security and quality -> Secrets and variables -> Actions"
    * Add the following secrets:
      * ```AWS_ACCESS_KEY_ID```
      * ```AWS_SECRET_ACCESS_KEY```
      * ```AWS_SESSION_TOKEN```
      * ```SSH_PRIVATE_KEY```
   * Paste the AWS access key ID, secret access key, and session token from the AWS Details panel into the corresponding secrets.
     *  Go to "AWS Academy -> Launch AWS Academy Learner Lab -> Start Lab"
     *  Once the lab is running, click "AWS Details -> AWS CLI -> Show"
     *  Copy and paste the corresponding data into each of the secrets
     *  Copy and paste the MC-Key you created earlier into the private key secret
     
### Should the user set environment variables or configure anything?
- The user does not need to set up variables or configure anything, the scripts do it all.

# Diagram
     ┌──────┐                  ┌──────┐                                       ┌───┐
     │GitHub│                  │Runner│                                       │EC2│
     └───┬──┘                  └───┬──┘                                       └─┬─┘
         │  Checkout Repository    │                                            │  
         │────────────────────────>│                                            │  
         │                         │                                            │  
         │      Creates EC2        │                                            │  
         │────────────────────────>│                                            │  
         │                         │                                            │  
         │                         │                  Creates                   │  
         │                         │───────────────────────────────────────────>│  
         │                         │                                            │  
         │                         │               Get Public IP                │  
         │                         │<───────────────────────────────────────────│  
         │                         │                                            │  
         │Install Ansible and nmap │                                            │  
         │────────────────────────>│                                            │  
         │                         │                                            │  
         │   Create Private Key    │                                            │  
         │────────────────────────>│                                            │  
         │                         │                                            │  
         │ Runs Ansible Playbook   │                                            │  
         │────────────────────────>│                                            │  
         │                         │                                            │  
         │                         │    Download/Install Java and Minecraft     │  
         │                         │───────────────────────────────────────────>│  
         │                         │                                            │  
         │                         │        Accepts the Minecraft Eula          │  
         │                         │───────────────────────────────────────────>│  
         │                         │                                            │  
         │                         │Creates the Minecraft User and Service File │  
         │                         │───────────────────────────────────────────>│  
         │                         │                                            │  
         │                         │   Installs and Starts Minecraft Server     │  
         │                         │───────────────────────────────────────────>│  
         │                         │                                            │  
         │     Workflow Done       │                                            │  
         │<────────────────────────│                                            │  
     ┌───┴──┐                  ┌───┴──┐                                       ┌─┴─┐
     │GitHub│                  │Runner│                                       │EC2│
     └──────┘                  └──────┘                                       └───┘
 [8]

# List of Commands to Run
- Everything is controlled from the GitHub action that runs the complete workflow. 
# How to connect to the Minecraft server once it's running?
- The ```setup-instance.yml``` script will automatically connect to the Minecraft server after it’s set up using the command: ```nmap -sV -Pn -p T:25565 <MC_IP>```
- In Minecraft, go to “Multiplayer -> Add Server” and enter the MC_IP in the “Server Address” box. Click “Done” and you’re ready to connect!

# References
**[1]** *Integrating with GitHub Actions – CI/CD Pipeline to Deploy a Web App to Amazon EC2 | AWS DevOps & Developer Productivity Blog.* 29 Mar. 2022, https://aws.amazon.com/blogs/devops/integrating-with-github-actions-ci-cd-pipeline-to-deploy-a-web-app-to-amazon-ec2/. 

**[2]** “Ansible with GitHub Actions: Automating Playbook Runs.” *Spacelift*, 13 Aug. 2024, https://spacelift.io/blog/github-actions-ansible. 

**[3]** *Describe-Instances — AWS CLI 2.35.2 Command Reference.* https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instances.html. 

**[4]** *Instance-Running — AWS CLI 2.35.2 Command Reference.* https://docs.aws.amazon.com/cli/latest/reference/ec2/wait/instance-running.html. 

**[5]** *Ansible Configuration Settings — Ansible Community Documentation.* https://docs.ansible.com/projects/ansible/latest/reference_appendices/config.html. 

**[6]** *Ansible.Builtin.Shell Module – Execute Shell Commands on Targets — Ansible Community Documentation.* https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/shell_module.html. 

**[7]** *Ansible.Builtin.Lineinfile Module – Manage Lines in Text Files — Ansible Community Documentation.* https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/lineinfile_module.html. 

**[8]** Vaughan, Arwen. “PlantText - Online PlantUML Editor for Fast UML Diagrams.” *PlantText*, https://www.planttext.com/.
