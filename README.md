# CS312-Course-Project
Automated Minecraft server on an EC2 instance.


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
