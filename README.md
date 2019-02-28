#  Ansible role for httpd/apache2 service
Ansible role for httpd/apache2 installation for CentOS 7

## What's inside?
1. Default config file: 
    ```
    /etc/httpd/conf/httpd.conf
    ```
2. Configuration files which load modules :
    ``` 
    /etc/httpd/conf.modules.d/ directory (e.g. PHP)
    ```
3. Select MPMs (Processing Model) as loadable modules [`worker`, `prefork` (default)] and `event`: 
    ```
    /etc/httpd/conf.modules.d/00-mpm.conf
    ```
4. Default ports: 
    ```
    80 and 443 (SSL)
    ```
5. Default log files:
    ``` 
    /var/log/httpd/{access_log,error_log}
    ```
6. The name of the user/group to run httpd as:
    ```
    User: apache
    Group: apache
    ```
7. `vagrant` user is added to `apache` group
8. Intention to make it fast for Magento 2. Currently no optimizations.
    -[ ] Strip LoadModule in /etc/httpd/conf* files
    -[ ] HostnameLookups turned off

## Tested on
Server version: Apache/2.4.6 (CentOS)

## Installation
1. Navigate to Ansible's roles folder
2. Add the repo to git modules
    ```
    git submodule add https://github.com/budnerp/ansible_role_apache2.git ansible_role_apache2
    ```
3. Add the role to Ansible's playbook file
    ```    
    roles:
    [...]
        - ansible_role_apache2
    [...]
    ```

## Other links
- Apache HTTP Server Project [https://httpd.apache.org/]()
- Multi-Processing Modules (MPMs) [https://httpd.apache.org/docs/2.4/mpm.html]()
- Apache MPM prefork [https://httpd.apache.org/docs/2.4/mod/prefork.html]()
- Comments section at [https://www.sonassi.com/blog/mythbusting/why-shouldnt-i-use-nginx-for-magento]()
- Archive article: Magento Performance Tuning Guidelines by Cignex Datamatix [https://www.cignex.com/blog/magento-performance-tuning-guidelines]()
- Tuning wydajności Apache [https://www.thomas-krenn.com/pl/wiki/Tuning_wydajno%C5%9Bci_Apache]()
- Strip Down Apache to Improve Performance & Memory Efficiency [https://haydenjames.io/strip-apache-improve-performance-memory-efficiency/]()
- Magento 2 - Set pre-installation ownership and permissions [https://devdocs.magento.com/guides/v2.3/install-gde/prereq/file-system-perms.html]()
- Magento 2 - Apache [https://devdocs.magento.com/guides/v2.3/install-gde/prereq/apache.html]()

## TO DO
-[x] Enable the Apache mod_rewrite and mod_version modules for Magento 2 (comes out of the box for ) 
    -[ ] s 
-[ ] Check if Magento 2 performance can be influenced by httpd MPM choice  
-[ ] Look into Magento 2 performance potential gain using: 
```
Inside: /etc/httpd/conf/httpd.conf
[...]
#
# EnableMMAP and EnableSendfile: On systems that support it,
# memory-mapping or the sendfile syscall may be used to deliver
# files.  This usually improves server performance, but must
# be turned off when serving from networked-mounted
# filesystems or if support for these functions is otherwise
# broken on your system.
# Defaults if commented: EnableMMAP On, EnableSendfile Off
#
#EnableMMAP off
EnableSendfile on
[...]
```

## License
Copyright (c) We Are Interactive under the MIT license.