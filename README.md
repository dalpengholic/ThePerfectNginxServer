# Nginx

### Linux Command
    - Visudo: add a user to the root group
    - Sudo: invoke root priileges
### Terminal Prompt
    - EX) root@hostname: ~ #
    - EX) username@hostname: ~$
    - root@hostname: ~ #
    - root: user name
    - hostname: server host name
    - ~: home directory:
    - #: root user
    - $: non root user
### Typing Commands
    - Hidden files: name starts with a period .ssh
    - ls -a: all files including hidden files
    - ls -l: listing
    - man ls: Manual of ls command
    - man cd: Manual of cd command
### File System Layout and Directories
    - /etc: where you find all of your configuration files
    - /home: for user created files and directories
    - /opt:  for installation of add on software packages 
    - /var:  contains data used by various application
    - Absolute Pathname: location is specified relative to the root directory
        - Start with /
    - Local Pathname: location is specified relative to the current directory
        - cd: home directory
        - cd /absolute_path
        - cd local_path
        - cd.. : parent directory
        - Cd -: previous directory
### Nano Editor
    - ^ shortcut: ctrl
    - M shortcut: alt
        - Mac user press esc instead of alt
    - ctr+G: help
    - ctr+W: search
    - ctr+X: exit
### Ownership and Permissions
    - / : owned by your user, writable by you user only, readable by web server
    - /wp-admin/: owned by your user, writable by you user only, readable by web server
    - /wp-includes/: owned by your user, writable by you user only, readable by web server
    - /wp-content/: owned by your user, writable by you user and the web server
    - Owner: 
        - user who creates the file
        - Any file or directory created by a user is automatically owned by that user
        - user group, same name is also created
    - Group owner:
        - Groups used to organize users different users can be added to groups
    - Other users:
        - Didn’t create the file
        - Not part of the group
    - r: read
    - w: write
    - x: execute
    - r: 4
    - w: 2
    - x: 1
    - No permission: 0
    - Ex) Permission 664
    - Owner: read+ write (rw-) 6
    - Group: read+ write (rw-) 6
    - Other: read (r—) 4
    - EX) Permission 775
    - O: read+ write+ execute (rwx) 7
    - G: read+ write+ execute (rwx) 7
    - O: read+ write+ execute (-wx) 5
    -  / : owned by your user, writable by you user only, readable by web server —> All user need to execute and read (1+4), only owner have write permission (7) -> 755
    -  /wp-admin/: owned by your user, writable by you user only, readable by web server —> 755
    -  /wp-includes/: owned by your user, writable by you user only, readable by web server —> 755
    -  /wp-content/: owned by your user, writable by you user and the web server—> 775
    - chmod: change the permission of a file or directory
    - usermod: modify the groups a user belongs to
    - chown: change the ow nership of files or directories
    - su: switch or change users
### Package and APT
    - Package: individual components that makes up al full featured software program
        - Ex) apt-cache depends <any package>
        - Dependencies: a package depends on  numerous smaller packages  
    - Repository:  servers that contains sets of packages. All packages are stored in what’s called repository
    - Package Manager: find and download and install the required dependencies for you
        - Ubuntu package manager: apt (advanced package manager)
    - Apt-get: configure packages
    - Apt-get update: synchronize the package files from the sources  (always update before using any other apt-get command)
    - Apt-get upgrade: install the newest versions of all packages currently installed on the system
    - `Apt-get dist-upgrade`: 
    - `Apt-get install < package_name>`:
    - `Apt-get remove`: doesn’t remove modified configuration file  
    - `Apt-get purge`: does remove modified configuration file

### First Login ROOT User
    - What is the server fingerprint?
        - When the operating system is installed on your server a unique I.D. for that particular server is generated and that unique I.D. is the server fingerprint.
        - When you accept the server fingerprint it is then stored locally on subsequent connections.SSH Will check and compare the locally stored fingerprint with that on the server. If they match the connection to the server will continue. If there is a mismatch you will be warned that the service fingerprint has changed.
        - If you reinstalled the servers operating system the mismatch is a consequence of that. If not be careful you may be subject to a man in the middle attack or even IP spoofing
        - Mac and Linux users, You will need to remove an existing server fingerprint if you reinstall the server operating system.
    - Change ROOT user at first login
    - Add a non root user to your server
    - the user must be given route privileges to use the command by visudo
    - Editing configuration files
    - Restarting services
    - `passwd`: changing a user’s password
    - `adduser`: adding a new user to your sever
    - `visudo`: giving a user root privilesges
    - `systemctl restart ssh`: restarting the ssh service
    - `logout or exit`: to logout of your sever
    - `Good Practice`: Making a backup copy of a configuration file
    - Ex) cp nameOfExistingfile NameOfNewFile
    - Adding the date to a backup file
    - /$(date +%Y-%m-%m)
    - Example of the copy command to create backup file
    - Ex) cp filename filename.$(date +%Y-%m-%m)
    - EX) cp filename filename.bak
    - At user privilege specification after `visudo`
        - `username ALL=(ALL:ALL) ALL`
        - First ALL: applies to our user logged in from all hosts
        - (ALL:ALL): specify our user can run commands as all users and groups
        - Last ALL: allows our user to run any commands
    - At /etc/ssh, make a backup copy before do configuration
### First Login NON ROOT User
    - `sudo`: using super user do for sever administrative tasks
    - `sudo apt-get update`: updating the servers package list
    - `sudo apt-get upgrade`: upgrading your server based on the package list
    - `sudo apt-get dist-upgrade`: dist-upgrade
    - `sudo reboot`: rebooting your server
    - `The following packages have been kept back:` We now have the message the following packages have been kept back. These are normally higher level patches to upgrade these packages. We need to use just upgrade. If ever you see any packages being held back run so you do get dist upgrade
    - When you run the dist upgrade command these are high level updates more often than not they require a reboot after the upgrade.
### SSH Key Authentication
    - Login using public/private key authentication
    - Key pair generated locally 
    - Public key stored on server
    - Private key stored locally
    - Keys are a pair
    - On local machine
        - `ssh-keygen`: create a ssh key pair
        - `chmod`: lock down access to your private key
        - `scp`: secure copy
            - `scp <path_of_public_key> <username@IPaddress:/<path_of_where_to_copy>>
    - On your server
        - `mkdir`: create a directory
            - `mkdir .ssh` at home directory
        - `mv`: Moving a file or directory
        - `mv`: Renaming a file or directory
            - `mv <pubkey> authorized_keys`
        - `chmod`: change permission
            - `chmod 400 authorized_keys` at .ssh
            - `chmod 700 .ssh` at home directory
        - `chattr`: changing the file attributes 
            - `sudo chattr +I authorized_keys`: I attribute cannot be modified deleted or rename.
        - `cd /etc/ssh` 
        - ‘sudo nano sshd_config`: We want to prevent anyone logging into our server using a password `cd /etc/ssh`  is where we find our servers configuration file
        - At authorizedKeysFile
            - Uncomment
            - Add `%h/.`: specifying that h must look at the user attempting to log in his home directory to locate the authorizedKeysFile in the `ssh` directory
        - At PasswordAuthentication 
            - `yes —> no`
        - Save
        - `sudo systemctl restart ssh`
        - `ssh -i <path_of_key> <username@IPaddress>
        - 
### Config Files
    ```
    Host udm
    Hostname 199.247.29.227
    User woojae-dev
    IdentityFile ~/.ssh/dovps
    ServerAliveInterval 60
    ServerAliveCountMax 120
    ```
    - Host: alias
    - HostName: IPaddress
    - User: User ID
    - IdentityFile: path to your private key
    - ServerAliveInterval : 60sec
    - ServerAliveCountMax 120
    - if you want to add an additional server. Press enter twice. Host give your server name.
    
   

### The firewall
- Control incoming and outgoing traffic
- Analyze data packets and determining whether they should be allowed or not
- Creating IPtable is very complex
- `sudo ufw status verbose`: check status of ufw
- `sudo ufw enable | sudo ufw disable`: enable or disable 
- `sudo ufw default deny incoming | allow outgoing`: default deny | allow rules
    - `sudo ufw deny incoming`
    - `sudo ufw allow outgoing`
- `sudo ufw allow`: ufw allow rules
    - `sudo ufw allow ssh`
    - `sudo ufw allow http`
    - `sudo ufw allow https`
    - `sudo ufw enable`
    - `sudo ufw status verbose`
- Configuration file: ufw
- Absolute path: /etc/default/ufw
- Ownership of file: root:root

### Fail2Ban
- Protect computer from brute force attacks
- Fail to ban operates by monitoring log files for selected entries and then it runs scripts based on those entries.
- Blocs selected ip addresses
- `sudo apt-get install fail2ban`
- `sudo systemctl restart | start | stop fail2ban`
- Configuration file: `jail.local` at `/etc/fail2ban/jail.loal
    - Ownership: root:root
- Log files
    - `fail2ban.log`: /var/log
    - `auth.log` : /var/log
    - `auth.log`: file the authorization log tracks usage of authorization systems to sodo command, remote logins, among others
    - Ownership:
        - `auth.log`: syslog:adm (permission 640)
        - `fail2ban`: root:adm (permission 640)
    - Need to add your user to ADM group
- `cp fail2ban.conf  fail2ban.local`: when it upgrade, we lose fail2ban.conf all we change inside. But fail2ban.local remains the same configuration
- `sudo usermod -a -G adm <username>`
- `sudo nano fail2ban.local` at /etc/fail2ban
    - Under miscellaneous section
    - `bantime`: how long a particular host is banned for
        - `findtime`:
        - `maxretry`: The max retry is the number of failures for a particular host will get banned.
    - Under Jain section
        - `sshd`: That is the jail that is protecting S-sh access.
- `sudo nano default-devian.conf` at /etc/fail2ban/jail.d
    - It's inside this particular file you specify. If you would like to enable or disable a particular Jayal currently only the SS H-L is an able.
### Install NGINX, MARIADB, and php7.2
    - Configuration file: `php.ini` at `/etc/php/7.2/fpm/php.ini
    - `sudo cp php.ini php.ini.bak`
    - `sudo nano php.ini`
        - Search using ctr+W
        - Search `allow_url_fopen` —> Off
        - Search `cgi.fix` and uncomment and edit `cgi.fix_pathinfo=0` 
        - Search `opcahce` and uncomment by removing ‘;’
        - Change `opcache.memory_consumption=192`
        - Change `opcache.interned_strings_buffer=16`
        - `opcache.max_accelerated_files=7963` a prime number
        - `opcache.validate_timestamps=0` and uncomment
        - `opcache.revalidate_freq=0`
    - `sudo systemctl restart php7.2-fpm`


### Overview of the NGINX Configuration to follow in the Course
- Configure nginx.conf
- Creating site directories
- Configure nginx server blocks
- Create database
- Install wpcli
- Install WordPress
- Secure WordPress site using command line
- Secure WordPress site using nginx directives
- Create ssl certificate using certbot
- Configure nginx “secure” server blocks
- Auto renew ssl certs

### DNS and Domain Names
- A Record: 
    - Host: @
    - Value: IP address
- CNAME Record:
    - Host: www
    - Value: domain name
- In order to access with domain name and www.domai name, set A record and CNAME Record
- If you want to subdomain, add additional A Record
    - EX) Host: shop
    - Value:  Server IP address

### context and directives
- `directive`: consists of an option and an option value and ends with a semi-colon
    - server_name domain.com www.domain.com;
- `context`: also a directive, but it encloses other directives in tis block
    - Events { worker_connections 767;}
- 5 main contexts: main, events, http, server, location
- `main`: main doesn’t have context {}
-  ‘Context’: open and end with curly bracket {}
- ‘event`: the events context is contained within the main context it sets Global Options that affect how engine X handles connections.
- `http`:  The HTTP context is contained in the main text the HTTP context enables and configures the HTTP service in engine X
- `server`: server context is contained within the HTTP context. The server context contains the configuration for virtual hosts. In Nginx terms,  virtual hosts referred to as the server block
-  `location`: the location context is contained within the server context. the location context lets you can figure our Nginx will respond to requests for resources with in the server.
- the location context is contained within the server context.

- When we look at the five main engine X contexts we have main events and HTTP inside the HTTP context you have the server context inside the server context. You have the location context when you look at this diagram the server context is a child of a HTTP and the location context is a child of the server context.
- When you work with engine X a directive in a child context will override the parent context so child context can override the directives in the parent context.
















