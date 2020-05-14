# SSH and Networking


### Port Basics
- Key Well-Known Ports
    - 21: FTP
    - 22: SSH 
    - 25: SMTP
    - 53: DNS
    - 80: HTTP
    - 110: POP3
    - 123: NTP
    - 443: HTTPS
- To check a port: `lsof -i:80` 

### SSH Basics
- The path of SSH configuration: `/etc/ssh/sshd_config`
    - #Port: the setting of Port of SSH. Default is 22


### To Connect to a Linux machine on Virtual Box 

- Install SSH server to the Linux machine:
    - `sudo apt-get update`
    - `sudo apt-get install openssh-server`

- Set port-forwarding 
    - Guest (Linux): 10.0.2.15, port 22
    - Host: for example, 127.0.0.1, port 22