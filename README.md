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

### Securing and Optimizing NGINX - Part 1 - The Main Nginx Configuration File
- `Nginx.conf` at `/etc/nginx/nginx/conf`: 
-  `sudo nano /etc/nginx/nginx/conf`: edit nginx.conf
- `lscpu`:  determine number of cpu cores
- `-ulimit -n`: determine number of worker connections
- `sudo nginx -t`: test nginx configuration file syntax before reload
- `sudo sysetemctl reload nginx` or `restart nginx`: reload/ restart nginx

- in the `main context`,
    -  `worker_processes`we set to the number of CPU cores your server has.
    - `worker_processes`: 1;
    - We will be adding `worker_rlimit_nofile` to the main context. We will be adding `worker_rlimit_nofile`  to the main context.This will help prevent that too many files open error that sometimes happens on busy sites.
    - `worker_rlimit_nofile`: 15000;
-  In the event context 
    - we will be modifying the work connections multi accept and `use epoll`.
    - The work connections value specifiers How many people can simultaneously be served by Nginx  by adding the worker are no file directive to the main context the worker connections directive can be increased beyond the system defaults by
    - `worker_connections 2048`
    - enabling multi except it causes engine X to immediately accept as many connections as it can.
    - `multi_accept on;`
    - epoll is recommended to increase throughput
    - `use epoll;`
- In `http context`
    -  `server_tokens`:  enables or disables nginx displaying the version of error page and in the server response hit a field.  We will disables theist prevent information leakage 
    -  `server_tokens off;`
    - `server_names_bucket_hash_bucket_size` uses hash tables, the size of a table is expressed in brackets. We are going to enable the server names hash packet size directive.
    - `server_names_bucket_hash_bucket_size 64;`
    -  2 log files: access_log, error_log
    - `access log file`: records every single request made to your server. on a busy site, this can translate into huge and resource demands. If you don't need the access log file and for a huge performance boost, disable the access log file.
    - `access_log off;`
    - `error_logfile`: The error log file must be kept as it's invaluable for troubleshooting 
    - `gzip compression`: by using GS compression as it's  that clients are requesting will be compressed. Therefore  smaller and faster to send
    - `gzip on;`
- we need to optimize the settings so as not to waste CPU cycles.
- Please do not attempt to compress asset? that's already compressed.
- JPEG files are already compressed and by attempting to compress them further you will probably end up with a larger file and you started with 
- buffers time outs and file handle caching.
    - If the buffer sizes are too low, Nginx will read and write to disk constantly, thereby reducing performance.
    - The following four directives will help with buffer sizes
    - `client_body_buffer_size`:    this reactive handles the client buffer size when Post actions are sent to Nginx.This is when forms are submitted.
    - `client_body_buffer_size 10k;`
    - `client_header_buffer_size`:  This directive handles the client header size 
    - `client_header_buffer_size 1k;`
    - `client_max_body_size`: This directive specifies the maximum allowed size for a client request. If the size is exceeded engine X will display a request entity too large error large 
    - `client_max_body_size 8m;`
    - `large_client_header_buffers`:  This directive ospecifies the maximum number and size of buffers for a large client.
    - `large_client_header_buffers 1k;`
- The purpose of servert timeouts is to prevent a device from endlessly waiting for a server to respond
    - `client_body_timeout` , `client_header_timeout`: These two directors are responsible for how long the server will wait for a client or client data to
    - be sent after the request 
    - `client_body_timeout 3m;`
    - `client_header_timeout 3m`
    - `keepalive_timeout`: this directive determines the time out for keepalive connections with the client the connection will close after this time period 
    - `keepalive_timeout 100;`
    - `send_timeout`:  sets a time out for transmitting a response to the client if the client does not receive anything within this time, The connection is closed 
    - `send_timeout 3m`
- `filehandle caching`: Opening a file can be a source of delay.Engine X can maintain a cache of open file descriptors for commonly served files thereby avoiding the delay.
    - `open_file_cache max=1000 inactive 20s;`
    - `open_file_cache_valid 30s;`
    - `open_fiel_cahche_min_uses 5;`
    - `open_file_cache_errors off;` 

- The file will handle cache does not cache the contents of a file but rather the file descriptors. When you open a file the operating system creates an entry to store information about the open file in the file descriptor table.
- what the engine X-File handle cache does. It caches the file handles too frequently requested files so this avoids the need for the operating system to reopen them again.
- The one downside is that engine X takes a little while to react to any changes you have made to any files 
- in the settings.
### Securing and Optimizing NGINX - Part 2 - The Main Nginx Configuration File
- At terminal `lscpu`
- `ulimit -n`
- `sudo nano nginx.conf`
- `sudo nginx -t`
- `sudo systemctl reload nginx`
### Securing and Optimizing NGINX - Part 3 - Buffers, Timeouts and the File Handle
- `open_file_cache max=1500 inactive=30s;` 
- `open_file_cache_valid 30s;`: nginx cache 1500 files for 30 seconds,  but that excludes any files that haven't been accessed for 30 seconds
- `open_file_cahce_min_uses 5;`: only files that have been accessed five times in that timeframe.
- 
### Creating the WordPress Directories to Store Your Site
- `server web root`: /var/www
- `ownership root:root` 
- `create directories`: <domain name>/public_html
- `using tree to view directory layout
- `chown -R user:group /path: changing ownership
- `mkdir`
- `mkdir -p`: create directory with sub-directories
- `sudo apt-get install tree`: install tree

### Configuring NGINX Server Blocks to Display Your WordPress Site - Part 1
- Configuration file: `default` at `/etc/nginx/sites-available/
- `sudo cp default default.bak`: create backup copy of the default file
- `sudo nano default`: open default file 
- `sudo find / -name php7.0-fpm.sock`: path to php7.0-fpm.sock file
- `sudo nginx -t`: test nginx configuration file syntax before reload
- `sudo systemctl reload nginx`: reload nginx
- 

### Configuring NGINX Server Blocks to Display Your WordPress Site - Part 2
- Location context is contained with the server context
- Location context is responsible for how nginx responds to requests for resources within the server
- Location match defines what nginx should check the requested uniform resources identifier(URI) against
- Existence of non existence modifier effects the way nginx attempts to match the location block
- Nginx location modifiers
    - Engine X processors requests based on whether there is a modifier or not in order of importance the order that engine X will process 
    - Order-Modifier-explanation
    - 1 - `=` - `exact match`
    - 2 - `^~` - preferential prefix match
    - 3 - `~ and ~*` - regex match: case sensitive and case insensitive match
    - 4 - - no modifier
- `exact match`: Site dot com slash favorites icon. In the location context,It says if an exact match for that particular file is made apply the expires directive. expires directive states that that file will be cached for one year.
- `preferential prefix match`: (^~)  Match is more important than a case sensitive or a case insensitive regular expression. If you have a location context with the carrot tool engine X we'll apply that context even if there is a better match through a regular expression.
- `case sensitive match` (~):  The tilt is a case sensitive regular expression match.
- `case insensitive match` (~*): If you look at the location context slash uploads ~* .uploads/.*\.php if somebody happens to upload a malicious PHP script to your server, and they then try and access that file, they will use site.com/uploads/a directory name followed by the name of the script. we are using a case insensitive match for anyone attempting to access a PHP file in your uploads directory. That case insensitive regular expression will match a file typed in uppercase and lowercase and apply the directive.  Deny all. They will not be able to run the HP file in your uploads directory.
- `no modifier`: no modifier is a prefix match.  how this works is when a request is made to your server,  Nginx will check for the file. Firstly at the url. Then if it doesn't find it. it will then look for a directory to match the request.mIf it doesn't find a file or directory, it then does an internal redirect to index.P P passing the query string arguments as parameters. as we start configuring the various directives inside the server blocks.

### Configuring NGINX Server Blocks to Display Your WordPress Site - Part 3
- Configuration files:
    - `default` at `/etc/nginx/sties-available/default`
    - `domain` at `/etc/nginx/sites-available/domain`

















