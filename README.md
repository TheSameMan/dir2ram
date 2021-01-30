# dir2ram
This repository contains a bash script for transferring folders with SSD to RAM and periodic backup to HDD in order to reduce unnecessary SSD rewriting cycles. 

## System requirements:
  Arch-based Linux (tested in Manjaro 20.2.1)
  SSD
  (>=) 8 GB RAM
  Free space on HDD (**should be auto-mountable for sync**)

## Instructions
The script contains the **src** list, which contains the paths to the cache folders and firefox profile. If necessary, this list is expanded with the additional folders. 

1. Fill **src** in the script file with the required directories. Set **dst** path to the folder on the HDD.

2. Transfer the script file to the system folder for subsequent automation
  `sudo mv /path/to/dir2ram /usr/bin/dir2ram`

3. Set the required script permissions 
  `sudo chown root:root /usr/bin/dir2ram`
  `sudo chmod 755 /usr/bin/dir2ram`

4. To automate, create (sample file attached) service file in /usr/lib/systemd/user/ 
  `sudo mv /path/to/dir2ram.service /usr/lib/systemd/user/dir2ram.service`

5. Set the required permissions
  `sudo chown root:root /usr/lib/systemd/user/dir2ram.service`
  `sudo chmod 644 /usr/lib/systemd/user/dir2ram.service`

6. Set the script to run at system startup 
  `systemctl --user daemon-reload`
  `systemctl --user enable dir2ram`
  `systemctl --user start dir2ram`

7. Set the script to run on login and logout 
  `echo '/usr/bin/dir2ram' | tee -a ~/.bash_logout ~/.bash_login > /dev/null`

8. For periodic backup on HDD, set the required sync interval 
  `crontab -e`
  Example synchronization in 1 hour
  `0 */1 * * * /usr/bin/dir2ram`


