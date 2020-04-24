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
- Apt-get dist-upgrade: 
- Apt-get install < package_name>:
- Apt-get remove: doesn’t remove modified configuration file  
- Apt-get purge: does remove modified configuration file



