# Assignment
##Installing Ghost and do the admin stuff

* add your public key to node to acces without password

* run the playbook ghost-install.yml with the -i option to select the hosts file
  (if you're testing in vagrant just run vagrant up(

* ssh to the box, su to ghostrider with the password 123

* cd to /var/www/ghost and run: `ghost install`
- when prompted you should answer
 - Enter your domain: (http://localhost:2368) `http://localhost`
 - Enter your MySQL hostname: (localhost) `ENTER`
 - Enter your MySQL username: `ghostuser`
 - Enter your MySQL password: [input is hidden]`ghostdb`
 - Enter your database name: (ghost_prod) `ghost`
 - Sudo Password [input is hidden]`123`
 - Do you wish to set up "ghost" mysql user? (Y/n) `n`
 - Do you wish to set up Nginx? (Y/n) `y`
 - Do you wish to set up Systemd? (Y/n)`y`
 - Do you want to start Ghost? (Y/n)`y`

* run `sudo systemctl restart nginx.service` (sometimes you have to remove /etc/nginx/sites-enabled/default)

* switch user to root and copy backup_ghost to the /root folder and add the following in `crontab -e`
  0 0 * * * ./backup_ghost
  this will backup /var/www/ghost and the MysqlDb to the backupfolder and send a mail with status
  (Remember to setup postfix and mailutils)

##Automation for developers

* now when your changed are ready for production run this playbook to update production (but first update with yor repo sttings)
