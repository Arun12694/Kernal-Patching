
# Kernal Patching #########

O.S. Patching on Production Server :-->	

***Pre-requisite-actions :	
Take Aprovals from Stake Holders	                                       - Infra-Team
Take Back-up of server before Patching	                                 - Infra-Team
Take App/DB backup if any	                                             - App/DB Team
Take Pre-patch report of respective servers	                           - Infra-Team
Pre-checks and take necessary config file on local system or jump host  - Infra-Team
Down the App /DB services on server	                                    - App/DB Team
Restart server for sanity check	                                       - Infra-Team
Start OS patching	                                                      - Infra-Team
do post check on OS end	                                                - Infra-Team
Sanity Check for App / DB	                                             - App/DB Team 

   
## Roll-Back Plan	
1> Boot server from old Kernal, each server required 1 hour downtime	     - Infra-Team

#############################################################################################

// All the kernal info is available in

/boot/grub/grub.conf

#############################################################################################

**Pre-requisite-comands :

# Pre-Check commands ########################################################################

yum list update
mount -a   //used to automatically mount all filesystems mentioned in the /etc/fstab, Reads the /etc/fstab configuration file and to mount all listed filesystems
df -hTP    //gives you a detailed snapshot of your mounted filesystems —> all with human-readable units and filesystem.
df -hTP >> /home/df_mountpoints.txt
cat /etc/hosts >> /home/hosts_bkp29072025
lsblk >> /home/lsblk_output_29072025 (Date)
yum update -y

# Post-Check Commands ########################################################################

mount -a    
ls /lib/modules
ls /lib/modules/3.10.0.1160.   //updated full package name
ls /lib/modules/3.10.0.1160/modules.dep
uname -r  //to check exiesting kernal package name before reboot
rpm -qa --last | grep kernel
mount -a
reboot -f   // to validate all the install updates
uname -r   // to check updated kernel version installed or not
df -hTP    //tocheck mount points
rpm -qa --last | grep -i kernel   //to check what are the updated packages installed
diff /home/hosts_bkp29072025 /etc/hosts
lsblk     //to display information about available or mounted block devices—like hard drives, SSDs, USB sticks, and their partitions.
cat /etc/hosts >> /home/hosts_bkp29072025
df -hTP     //tocheck mount points
cat /home/df_mountpoints.txt

# Roll Back packages (if required) ############################################################

yum history|head -n 7
yum history undo (ID No.)








