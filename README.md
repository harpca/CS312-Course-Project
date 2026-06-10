# CS 312 Course Project Part 2
## What will we do?
- Run the GitHub action workflow to create and run an automated Minecraft server.
## How will we do it?
- The solution consists of two files:
  * **The GitHub action workflow:** setup-instance.yml
  * **The Ansible playbook:** install-MC.yml

# Requirements
### What will the user need to configure to run the pipeline?
- 
### What tools should be installed?
- 
### Are there any credentials or CLI required?
- 
### Should the user set environment variables or configure anything?
- 

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

# List of Commands to Run
- 
# How to connect to the Minecraft server once it's running?
- 
# References
- 
