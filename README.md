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
    - 

















