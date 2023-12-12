```
practise server :


main pr : 54.196.17.223

m1: 54.85.252.119

m2: 18.232.107.57

```

# ansible-lumen-tr


```
ansible / terraform :

configuration / provisioning 


50 servers  -- memory infra   -- package 10
5 rds
5 sg


3 servers : 

CentOS 7 (x86_64) - with Updat...read more
ami-002070d43b0a4f171
Virtual server type (instance type)
t2.micro
Firewall (security group)
raman-sg
Storage (volumes)
1 volume(s) - 10 GiB






keypair : pem : cmd , gitbash
terminal


C:\Users\techlanders>cd Downloads

C:\Users\techlanders\Downloads>ssh -i "raman-nvirgnia.pem" centos@ec2-54-80-107-70.compute-1.amazonaws.com
The authenticity of host 'ec2-54-80-107-70.compute-1.amazonaws.com (54.80.107.70)' can't be established.
ED25519 key fingerprint is SHA256:gOpfePCR1bS70ARxOqsCnHOR47HIDNM2pzlVKvbaBmc.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'ec2-54-80-107-70.compute-1.amazonaws.com' (ED25519) to the list of known hosts.
[centos@ip-172-31-40-174 ~]$ sudo -i
[root@ip-172-31-40-174 ~]#






ppk : putty




---------------------------------------

on main node :

install ansible 


source : pvtkey ,, windows 

dest : publickey ,, aws cloud



----------------------------------------


on master node :

creating a keypair

 rm -rf raman.pem
   50  clear
   51  ssh-keygen -t rsa
   52  ls -a
   53  cd .ssh/
   54  ls
   55  cat id_rsa
   56  clear
   57  ls
   58  ssh copy-id root@3.86.15.41
   59  ssh-copy-id root@3.86.15.41


for testing :
ssh root@3.86.15.41
and u will be able to ssh into m1 passwrdlessly

on m1 :

 passwd root   
    3  vi /etc/ssh/sshd_config
    4  systemctl restart sshd
    5  pwd
ssh-copy-id root@3.86.15.41 ( on main )
    6  ls -a
    7  cd .ssh/
    8  ls
    9  cat authorized_keys






```

```

passwordless authentication :

clear
   79  ls
   80  pwd
   81  mkdir raman
   82  cd raman/
   83  ls
   84  vi inv
   85  ls
   86  pwd
   87  ls
   88  vi /etc/ansible/ansible.cfg
   89  ansible 52.203.201.127 -m ping
   90  vi /etc/ansible/ansible.cfg
   91  ansible 52.203.201.127 -m ping -i inv
   92  ls
   93  vi inv
   94  ansible all -m ping
   95  ansible all -m ping -i inv
   96  vi /etc/ansible/ansible.cfg
   97  cat inv
   98  vi /etc/ansible/hosts
   99  clear
  100  ansible all -m ping
  101  ansible all -m ping -i /root/raman/inv
  102  clear
  103  ansible demo -m ping -i /root/raman/inv






ansible ad hoc commands :




cat inv
  109  vi /etc/ansible/hosts
  110  ansible demo -m ping -i /root/raman/inv
  111  ansible demo -m ping
  112  cat /etc/ansible/hosts
  113  clear
  114  ls
  115  cd ..
  116  ls
  117  cd raman/
  118  ls
  119  ansible demo -a "ls"
  120  ansible demo -a "ls" -i inv
  121  ansible demo[0] -a "ls" -i inv
  122  ansible demo[1] -a "ls" -i inv
  123  ansible demo[0:5] -a "ls" -i inv
  124  ansible demo[-1] -a "ls" -i inv
  125  clear
  126  ansible demo --list-hosts
  127  ansible demo --list-hosts -i inv
  128  ansible demo -a "touch myfile"
  129  ansible demo -a "touch myfile" -i inv
  130  ansible demo -a "ls" -i inv
  131  ansible demo -a "ls -ltr" -i inv
  132  ansible demo -a "ls -la" -i inv
  133  ansible demo -a "rm -rf myfile" -i inv
  134  clear
  135  ansible demo -a "yum install httpd -y" -i inv
  136  ansible demo -a "which httpd" -i inv
  137  ansible demo -a "systemctl start httpd" -i inv
  138  ansible demo -a "yum install httpd -y" -i inv
  139  clear
  140  ansible -h
  141  clear
  142  ansible demo -a "yum remove httpd -y" -i inv
  143  clear
  144  ansible -h
  145  clear
  146  history
  147  clear
  148  ansible -h
  149  clear
  150  ls
  151  vi raman.pem
  152  ls
  153  ls -a
  154  cd /root/
  155  ls -a
  156  cd .ssh
  157  ls
  158  cd /root/raman/
  159  ls
  160  ansible -h
  161  clear
  162  ansible demo -i inv -m ping --private-key=raman.pem
  163  ls
  164  chmod 400 raman.pem
  165  ansible demo -i inv -m ping --private-keyraman.pem
  167  ansible -h
  168  ansible demo -i inv -m ping --private-key raman.pem -u centos


  177  ansible demo -i inv -m ping --private-key raman.pem -u centos -b
  178  ansible -h
  179  ansible demo -i inv -m ping --private-key raman.pem -u centos -b --become-user=raman





ansible modules :


 ansible-doc -l
  208  cd /usr/bin/
  209  ls
  210  ls ls
  211  clear
  212  cd /root/raman/
  213  ls
  214  rm -rf raman.pem
  215  clear
  216  ls
  217  ansible all -m ping -i inv
  218  clear
  219  ansible-doc -l | grep ping
  220  clear
  221  ansible-doc -v ping
  222  clear
  223  ansible-doc -l | grep user
  224  clear
  225  ansible -m user -a "name=khanna comment=\"created via ansible cli\" group=root shell=/bin/bash"
  226  ansible demo -i inv -m user -a "name=khanna comment=\"created via ansible cli\" group=root shell=/bin/bash"
  227  ansible demo -m setup
  228  clear
  229  ansible demo -m setup -i inv
  230  clear
  231  ansible all  -i inv -m user -a "name=raman state=absent
  232  ansible all  -i inv -m user -a "name=raman state=absent"
  233  ansible all  -i inv -m user -a "name=khanna state=absent"
  234  clear
  235  ansible all  -i inv -m yum -a "name=telnet state=present"
  236  ansible all  -i inv -m yum -a "name=telnet state=absent"
  237  clear
  238  ansible demo -i inv -m file -a "path=/tmp/ramankhanna state=directory mode=777"
  239  ansible demo -i inv -m file -a "path=/tmp/ramankhanna state=file mode=777"
  240  ansible demo -i inv -m file -a "path=/tmp/ramankhanna1 state=file mode=777"
  241  ansible demo -i inv -m file -a "path=/tmp/ramankhanna state=touch mode=777"
  242  ansible demo -i inv -m file -a "path=/tmp/ramankhann1a state=touch mode=777"
  243  clear
  244  ansible demo -i inv -m setup -a "filter="nsible-distribution"
  245  ansible demo -i inv -m setup -a "filter=ansible-distribution"
  246  ansible demo -i inv -m setup | grep public
  247  clear
  248  ansible-doc -l
  249  clear
  250  ansible demo -i inv -m uptime
  251  ansible-doc -l | grep uptime
  252  ansible demo -m package -a "name=telnet state=present"
  253  clear
  254  ansible client -m copy -a "src=/tmp/myfile dest=/root mode=777"
  255  ansible all -i inv -m copy -a "src=/tmp/myfile dest=/root mode=777"
  256  touch /tmp/myfile
  257  ansible all -i inv -m copy -a "src=/tmp/myfile dest=/root mode=777"
  258  ansible all -i inv -m shell -a "ls;uname -a"









ansible playbook

```



```

playbooks (.yaml/yml) -- workflow of ansible

  plays ,,,
    
     tasks



vi xyz.yml

- hosts: webservers
  remote_user: yourname
  become: yes
  become_user: postgres
  tasks 
  -- installing pckage
  -- starting

v   



---


- hosts: appservers
  remote_user: yourname
  become: yes
  become_user: postgres
  tasks 


  dfb
b  bgn






-------------------------------------------------------------


[root@main raman]# cat target.yml
---
- hosts: demo
  user: centos
  become: yes
  connection: ssh
  gather_facts: yes
[root@main raman]# cat tasks.yml
---
- hosts: demo
#  user: centos
#  become: yes
#  connection: ssh
#  gather_facts: yes
  tasks:
  - name: installation of httpd
    action: yum name=httpd state=absent
  - name: addition of file
    action: file path=/opt/testdir state=directory
#Lab5: Working with Playbook
  - name: group creation
    group:
      name: grouptest
      gid: 5555
  - name: second group creation
    group:
      name: grouptest2
      gid: 6666




ansible -h
  273  clear
  274  ls
  275  vi target.yml
  276  ls
  277  ansible-playbook -i inv target.yml
  278  vi target.yml
  279  cat inv
  280  ansible -m ping -i inv -u centos -b
  281*
  282  ls
  283  cd /root/.ssh/
  284  ls
  285  cat known_hosts
  286  clea
  287  clear
  288  vi raman.pem
  289  cd /root/raman/
  290  ls
  291  vi raman.pem
  292  ls
  293  ansible -m ping -i inv -u centos -b --private-key raman.pem
  294  ansible demo -m ping -i inv -u centos -b --private-key raman.pem
  295  chmod 400 raman.pem
  296  ansible demo -m ping -i inv -u centos -b --private-key raman.pem
  297  clear
  298  ansible-playbook -i inv --private-key raman.pem target.yml
  299  cat target.yml
  300  clear
  301  cat target.yml
  302  vi tasks.yml
  303  ansible-playbook -i inv --private-key raman.pem tasks.yml
  304  vi tasks
  305  vi tasks.yml
  306  vi /etc/ansible/ansible.cfg
  307  vi tasks.yml
  308  ansible-playbook -i inv tasks.yml
  309  vi tasks.yml
  310  ansible-playbook -i inv tasks.yml
  311  cat tasks
  312  cat tasks.yml
  313  clear
  314  vi tasks.yml
  315  ansible-playbook -i inv tasks.yml
  316  cat tasks.yml
  317  vi tasks.yml
  318  clear
  319  ansible-playbook -i inv tasks.yml
  320  vi tasks.yml
  321  ansible-playbook -i inv tasks.yml
  322  vi tasks.yml
  323  ansible-playbook -i inv tasks.yml
  324  vi tasks.yml
  325  ansible-playbook -i inv tasks.yml
  326  clear
  327  vi tasks.yml
  328  ansible-playbook -i inv tasks.yml


---



lab6:

Create a Playbook for User and Group Creation with user name "usertest", shell bash, userid 6666 and pass the comments as "my first user". Group details will be name "grouptest" and group id 7777.

Create a Playbook for files and directories:
create a directory with root ownership; inside this directory, create one file with “test” with ownership of usertest (the user we have created in 1st example). Copy some content into the newly created file.



[root@main raman]# cat lab6.yml
---
- name: create user ,group, file and dir
  hosts: demo
  become: yes
  tasks:
  - name: create a group
    group: name=grouptest gid=7777 state=present
  - name: create a user
    user: name=usertest shell=/bin/bash state=present comment="my first user" uid=6666 group=grouptest

  - name: create a directory
    file: path=/tmp/rktest state=directory owner=root group=root mode=0755
  - name: create a file and copy some content
    copy:
      content: "This is the file created with copy. "
      dest: /tmp/rktest/rktestfile
      owner: usertest
      group: grouptest
      mode: 0644





 ansible-playbook -i inv lab6.yml --check
  364  ansible-playbook -i inv lab6.yml





-------------------------------
handlers :






1
2    made some change (hndlers) ,notify
3
4
5
6
7


handlers( operation)


[root@main raman]# cat ntp.yml
- hosts: all
  tasks:
  - name: ntp os package instalation
    package: name=ntp state=present
  - name: ntp file configurations
    file: path=/etc/ntp.conf state=file
  - name: to start ntp svc
    service: name=ntpd state=started enabled=yes  





[root@main raman]# cat ntp.yml
- hosts: all
  tasks:
  - name: ntp os package instalation
    package: name=ntp state=present
  - name: ntp file configurations
    file: path=/etc/ntp.conf state=file
    notify:
    - restart the ntp svc on changes in ntp configuration
  - name: to start ntp svc
    service: name=ntpd state=started enabled=yes
  handlers:
  - name: restart the ntp svc on changes in ntp configuration
    service: name=ntpd state=restarted



[root@main raman]# cat ntp.yml
- hosts: all
  tasks:
  - name: ntp os package instalation
    package: name=ntp state=present
  - name: ntp file config from my local to remote dest
    copy: src=./ntp.conf dest=/etc/ntp.conf
    notify:
    - restart the ntp svc on changes in ntp configuration
  - name: to start ntp svc
    service: name=ntpd state=started enabled=yes
  handlers:
  - name: restart the ntp svc on changes in ntp configuration
    service: name=ntpd state=restarted


----


vi ntp.yml
  373  ls
  374  ansible-playbook -i inv lab6.yml--syntax-check
  375  ansible-playbook -i inv ntp.yml --syntax-check
  376  vi ntp.yml
  377  ansible-playbook -i inv ntp.yml --check
  378  ansible-playbook -i inv ntp.yml
  379  clear
  380  vi ntp.yml
  381  cat ntp.yml
  382  clear
  383  ansible-playbook -i inv ntp.yml
  384  vi ntp.yml
  385  cat ntp.yml
  386  ansible-playbook -i inv ntp.yml
  387  ls
  388  vi ntp.conf
  389  ansible-playbook -i inv ntp.yml
  390  vi ntp.yml
  391  vi ntp.conf
  392  ansible-playbook -i inv ntp.yml
  393  cat ntp.
  394  cat ntp.yml
  395  ansible-doc -v package
  396  clear
  397  cat ntp.yml
  398  cat ntp.conf
  399  ansible-playbook -i inv ntp.yml
  400  cat ntp.conf
  401  vi ntp.conf
  402  ansible-playbook -i inv ntp.yml

Handlers primary use cases is to restart services, handlers can serve various purposes beyond service restarts, such as:

Configuration file updates: After modifying a configuration file, a handler can be used to trigger a service reload or restart to apply the changes.

Package installations: After installing new packages, a handler can be used to restart services or perform further configuration updates that depend on the installed packages.

Restarting servers: Handlers can be employed to restart servers or perform maintenance activities on servers after specific configurations or changes have been applied.

Sending notifications: They can be used to trigger notifications, such as sending emails or messages to alert administrators or users about changes or tasks completion.

Managing firewall rules: Handlers can be used to reload firewall configurations or restart firewalls after applying rule changes.

Deployments and updates: After deploying or updating an application, handlers can be used to execute tasks like clearing caches, reloading configurations, or restarting services.

Database operations: Performing database-related tasks such as schema updates, reloading configurations, or restarting the database service.

```





```

[root@main raman]# cat variable.yml
---
- hosts: demo
  connection: ssh
  vars:
#    pkg: tree
    pkg: httpd
  tasks:
  - name: installation of tree/yum pkg
    yum: name={{ pkg }} state=installed




ansible-playbook -i inv variable.yml --syntax-check
  419  ansible-playbook -i inv variable.yml --check
  420  ansible-playbook -i inv variable.yml
  421  vi variable.yml
  422  ansible-playbook -i inv variable.yml
  423  vi variable.yml
  424  ansible-playbook -i inv variable.yml


--------------------------------------------

[root@main raman]# cat variable.yml
---
- hosts: demo
  connection: ssh
  vars:
#    pkg: tree
    pkg: httpd
    us1: gagan2
    uid1: ""
    us2: raman
    uid2: 8765
  tasks:
  - name: installation of tree/yum pkg
    yum: name={{ pkg }} state=installed
  - name: creating user1
    user: name={{ us1 }} uid={{ uid1 }}
  - name: creating user2
    user: name={{ us2 }} uid={{ uid2 }}



 ansible-playbook -i inv variable.yml -e uid1=8764
  446  vi variable.yml
  447  ansible-playbook -i inv variable.yml -e uid1=8763
  448  vi variable.yml
  449  cat variable.yml


------------------------------------


- hosts: all
  vars:
    pkg: ntp
    svc: ntpd
  tasks:
  - name: installing {{ pkg }}
    package:
      name: "{{ pkg }}"
      state: installed
  - name: file {{ pkg }} config from my local to remote dest
    copy: src=./ntp.conf dest=/etc/ntp.conf
    notify:
    - restarthandler
  - name: to start {{ pkg }} {{ svc }}
    service: name="{{ svc }}" state=started enabled=yes
  - name: configuration successfully done on hosts
    debug: msg="Playbook ran successfully on host {{ ansible_hostname }}"
  handlers:
  - name: restarthandler
    service: name="{{ svc }}" state=restarted




vi ntp.yml
  486  clear
  487  ansible -i inv -m setup -a "filter=ansible_hostname"
  488  ansible demo -i inv -m setup -a "filter=ansible_hostname"
  489  vi ntp.yml
  490  clear
  491  ansible-playbook -i inv ntp.yml
  492  vi ntp.conf
  493  ansible-playbook -i inv ntp.yml
  494  clear


------------------------------------------------------

[root@main raman]# cat lab8.yml
---
- hosts: all
  vars:
    httpd_package: httpd
  tasks:
  - name: install httpd package
    package:
      name: "{{httpd_package}}"
      state: present
  - name: start httpd service
    service:
      name: httpd
      state: started
  - name: config appache config port change
    lineinfile:
      path: /etc/httpd/conf/httpd.conf
      regexp: "Listen 80"
      line: "Listen 81"
  - name: add static config to servers
    copy:
      dest: /var/www/html/index.html
      content: "<h1> this is a demo for apache webserver hosted on {{ ansible_hostname }} and of os : {{ ansible_os_family }} !</h1>"
    notify: restart httpd
  handlers:
  - name: restart httpd
    service:
      name: httpd
      state: restarted
      enabled: yes

[root@main raman]# cat lab8.1.yml --- -... by Raman Khanna
12:26 PM
Raman Khanna
[root@main raman]# cat lab8.1.yml
---
- hosts: all
  vars:
    httpd_package: httpd
  tasks:
  - name: install httpd package
    package:
      name: "{{httpd_package}}"
      state: present
  - name: start httpd service
    service:
      name: httpd
      state: started
  - name: config appache config port change
    lineinfile:
      path: /etc/httpd/conf/httpd.conf
      regexp: "Listen 80"
      line: "Listen 81"
  - name: add static config to servers
    template:
      src: index.html
      dest: /var/www/html/index.html
    notify: restart httpd
  handlers:
  - name: restart httpd
    service:
      name: httpd
      state: restarted
      enabled: yes

[root@main raman]# cat index.html <html> <h... by Raman Khanna
12:26 PM
Raman Khanna
[root@main raman]# cat index.html
<html>
<head>
<title>Server Information</title>
</head>
<body>
<h1> this is a demo for webserver hosted on {{ ansible_hostname }} and of os : {{ ansible_os_family }} !</h1>
</body>
</html>

-------------------------------------------------




[root@main raman]# cat factset.yml
---
- name: This is my First Debug Play
  hosts: all
  tasks:
    - name: Testing Ansible Facts {{ ansible_hostname }}
# My task with outputs fetched from Facts
      debug: msg="Host {{ ansible_hostname }} is having IP address {{ ansible_eth0.ipv4.address }}"
    - debug: msg="second task"
    - debug: msg="system {{ inventory_hostname }} has uuid {{ ansible_product_uuid }}"






[root@main raman]# cat debug-register.yml
---
- name: debug play
  hosts: all
  tasks:
  - name: talk package install
    yum: name=telnet state=present
    register: output

  - name: running debugger to show output
    debug: var=output




[root@main raman]# cat ntp.yml
- hosts: all
  vars:
    pkg: ntp
    ansible_hostname: ntpd
  tasks:
  - name: installing {{ pkg }}
    package:
      name: "{{ pkg }}"
      state: installed
    register: ntp_out
  - name: file {{ pkg }} config from my local to remote dest
    copy: src=./ntp.conf dest=/etc/ntp.conf
    notify:
    - restarthandler
  - name: to start {{ pkg }} {{ ansible_hostname }}
    service: name="{{ ansible_hostname }}" state=started enabled=yes
  - name: configuration successfully done on hosts
    debug: msg="Playbook ran successfully on host {{ ansible_hostname }}"
  - name: printing complete output
    debug: var=ntp_out
  - name: printing specific result for indivod paameter
    debug: var=ntp_out.changed
  handlers:
  - name: restarthandler
    service: name="{{ ansible_hostname }}" state=restarted



--------------------------------------------------------------------------

```


```

 


[root@main raman]# cat ignore_error.yml
---
- name: ignore error
  hosts: demo
  tasks:
  - name: error task
    command: /bin/date12
    ignore_errors: yes
  - name: second task
    service: name=ntpd state=started








[root@main raman]# cat ignore2.yml
- hosts: demo
  vars:
    pkg: ntp
    ansible_hostname: ntpd
  tasks:
  - name: task1 - run a command
#    command: /dev/null
    command: ls
    ignore_errors: true
    register: task1_result

  - name : debug task1 result
    debug: var=task1_result

  - name: installing {{ pkg }}
    package:
      name: "{{ pkg }}"
      state: installed
    register: ntp_out

  - name: to start {{ pkg }} {{ ansible_hostname }}
    service: name="{{ ansible_hostname }}" state=started enabled=yes

  - name: final task - run only if task1 fails
    debug: msg="this task runs only if task1 fails"
    when: task1_result.failed



===================================================================





---
- name: Conditional checks
  hosts: all
  tasks:
    - name: Installing web packages on all centos version 7 servers
      yum: name=httpd state=installed
      when: ansible_distribution == “CentOS” and ansible_distribution_major_version == “7”


#### dnt try :

 - name: "shut down CentOS 6 and Debian 7 systems"
    command: /sbin/shutdown -t now
    when: (ansible_facts['distribution'] == "CentOS" and ansible_facts['distribution_major_version'] == "6") or
          (ansible_facts['distribution'] == "Debian" and ansible_facts['distribution_major_version'] == "7")
###







[root@main raman]# cat ntp.yml
- hosts: demo1
  vars:
#    pkg: ntpd
    pkg: ntp
    ansible_hostname: ntpd
  tasks:
  - name: installing {{ pkg }}
    package:
      name: "{{ pkg }}"
      state: installed
    ignore_errors: yes
    register: ntp_out
  - name: print installation summary
    debug: var=ntp_out
#    when: ntp_out.rc != 0
    when: ntp_out.rc == 0
  - name: file {{ pkg }} config from my local to remote dest
    copy: src=./ntp.conf dest=/etc/ntp.conf
    notify:
    - restarthandler
  - name: to start {{ pkg }} {{ ansible_hostname }}
    service: name="{{ ansible_hostname }}" state=started enabled=yes
  - name: configuration successfully done on hosts
    debug: msg="Playbook ran successfully on host {{ ansible_hostname }}"
  - name: printing complete output
    debug: var=ntp_out
  - name: printing specific result for indivod paameter
    debug: var=ntp_out.changed
  handlers:
  - name: restarthandler
    service: name="{{ ansible_hostname }}" state=restarted







[root@main raman]# cat conditions.yml
- hosts: all
  tasks:
  - name: Register a variable
    package: name=ntp state=installed
    register: ntp_out
    ignore_errors: true
  - name: debug
    debug:
      var: ntp_out
  - name: Use the variable in conditional statement
    shell: echo "motd contains the word ansible"
    when: ntp_out.rc == 0
    register: echo_output

  - name: Display echoed message
    debug:
      var: echo_output.stdout

  - name: Register a variable
    shell: cat /etc/motd
    register: motd_contents

  - name: Use the variable in conditional statement
    shell: echo "motd contains the word hi"
    when: motd_contents.stdout.find('hi') != -1
    register: echo_output

  - name: Display echoed message
    debug:
      var: echo_output.stdout


========================================================================





[root@main raman]# cat conditions2.yml
- name: Conditional checks
  hosts: all
  tasks:
  - name: creation of user
    user: name=ramanlumen state=present
    when: ansible_distribution == 'CentOS' and ansible_distribution_version == '7.9'
    register: user_out
  - name: false_task
    debug: var=user_out
    ignore_errors: true
    when: user_out.rc == 0
  - name: creating a file on servers
    file: path=/tmp/rks state=touch mode=1600
    when: ansible_distribution == 'Redhat' and ansible_distribution_version == '8'







[root@main raman]# cat loop.yml
- hosts: all
  tasks:
  - name: create multiple users with loop
    user: name="{{ item }}" state=present shell=/bin/bash
    loop: [gagan1,gagan2,gagan3,gagan4]
#   loop:
#   - gagan1
#   - gagan2
  - name: second task loop with condition
    command: echo {{ item }}
    loop: [1,3,5,7,8,9]
    when: item >=2






[root@main raman]# cat loop2.yml
- hosts: all
  tasks:
  gather_facts: true
# gather_facts: false
  tasks:
  - name: check centos version
    command: cat /etc/os-release
    register: centos_version
  - name: install pckages
    package: name="{{ item }}" state=present
    loop: [php,gcc,talk,tree,vim,httpd]
    when: ansible_distribution == 'CentOS' or ansible_distribution_version == '7.8'







[root@main raman]# cat loop2.yml
- hosts: all
  tasks:
  gather_facts: true
# gather_facts: false
  tasks:
  - name: check centos version
    command: cat /etc/os-release
    register: centos_version
  - name : output centos version
    debug: var=centos_version
  - name: install pckages
    package: name="{{ item }}" state=present
    loop: [php,gcc,talk,tree,vim,httpd]
#    when: ansible_distribution == 'CentOS' or ansible_distribution_version == '7.8'
#    when: centos_version.stdout.find('CentOS Linux 7') != -1
    when: centos_version.stdout.find('Ubuntu') != -1





===================================================================================================






```



```

playbook

play :

set of operations :

block :
  1 : apply on individual tasks
  2
  3
  4
  5
  6
  7
 when (any condition)
rescue: errro handling 




---
- name: instalation
  hosts: demo
  tasks:
  - name: block run
    block:
    - name: installing telnet package
      yum: name=teln state=installed
      register: result
    - name: print output
      debug: var=res
    rescue:
    - name: handle errors
      debug: msg="an erorr occured while installing telnet pkg"
    when: ansible_distribution=="CentOS"
    ignore_errors: false
  - name: add user
    user: name=redhtuser state=present
    when: ansible_distribution=="CentOS"



========================================================================================


 mkdir roles
  796  cd roles/
  797  ls
  798  tree
  799  ansible-galaxy init ramanrole
  800  ls
  801  tree
  802  clear
  803  ls
  804  cd ramanrole/
  805  ls
  806  cd tasks/
  807  s
  808  ls
  809  vi main.yml
  810  cd defaults
  811  cd ..
  812  ls
  813  cd defaults/
  814  ls
  815  vi main.yml
  816  cd ..
  817  ls
  818  cd vars/
  819  ls
  820  vi main.yml
  821  tree
  822  cd ..
  823  tree
  824  clear
  825  ls
  826  cd ..
  827  ls
  828  cd ..
  829  ls
  830  cp inv roles/
  831  cd roles/
  832  ls
  833  vi ramanrole.yml
  834  ls
  835  ansible-playbook -i inv ramanrole.yml




[root@main roles]# tree
.
├── inv
├── ramanrole
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── README.md
│   ├── tasks
│   │   └── main.yml
│   ├── templates
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
└── ramanrole.yml

9 directories, 10 files






[root@ansible-controller role]# cat defaults/main.yml
---
# defaults variable file for file for gaganrole
user:
  gagandeep
uid:
  7654

Note: make sure, not to write "vars" on top.






[root@ansible-controller role]# cat tasks/main.yml
---
# tasks file for gaganrole
- name: Creating {{user}}
  user: name={{user}} uid={{uid}} state=present
  register: outputs
- name: Checking outputs
  debug: var=outputs

Note: make sure, not to write "tasks" on top.






root@ansible-controller playbooks]# cat gaganroletest.yml
---
- name: Testing role
  hosts: all

# Define roles here
  roles:
    - gaganrole






=========================================================================

- hosts: demo1
  vars:
#    pkg: ntpd
    pkg: ntp
    svc: ntpd
  tasks:
  - name: installing {{ pkg }}
    package:
      name: "{{ pkg }}"
      state: installed
    ignore_errors: yes
    register: ntp_out
  - name: print installation summary
    debug: var=ntp_out
#    when: ntp_out.rc != 0
    when: ntp_out.rc == 0
  - name: file {{ pkg }} config from my local to remote dest
    copy: src=./ntp.conf dest=/etc/ntp.conf
    notify:
    - restarthandler
  - name: to start {{ pkg }} {{ ansible_hostname }}
    service: name="{{ svc }}" state=started enabled=yes
  - name: configuration successfully done on hosts
    debug: msg="Playbook ran successfully on host {{ ansible_hostname }}"
  - name: printing complete output
    debug: var=ntp_out
  - name: printing specific result for indivod paameter
    debug: var=ntp_out.changed
  handlers:
  - name: restarthandler
    service: name="{{ ansible_hostname }}" state=restarted








http-role :






- hosts: all
  vars:
    httpd_package: httpd
  tasks:
  - name: install httpd package
    package:
      name: "{{httpd_package}}"
      state: present
  - name: start httpd service
    service:
      name: httpd
      state: started
  - name: config appache config port change
    lineinfile:
      path: /etc/httpd/conf/httpd.conf
      regexp: "Listen 80"
      line: "Listen 81"
  - name: add static config to servers
    template:
      src: index.html
      dest: /var/www/html/index.html
    notify: restart httpd
  handlers:
  - name: restart httpd
    service:
      name: httpd
      state: restarted
      enabled: yes




============================================================================================




[root@main http-role]# cd defaults/
[root@main defaults]# ls
main.yml
[root@main defaults]# cat main.yml
---
# defaults file for http-role
httpd_package: httpd





[root@main http-role]# cd handlers/
[root@main handlers]# ls
main.yml
[root@main handlers]# cat main.yml
---
# handlers file for http-role
- name: restart httpd
  service:
    name: httpd
    state: restarted
    enabled: yes






[root@main http-role]# cd tasks/
[root@main tasks]# cat main.yml
---
# tasks file for http-role
  - name: include nested ntp role in this as first task
    include_role: name=ntp-role

  - name: install httpd package
    package:
      name: "{{httpd_package}}"
      state: present
  - name: start httpd service
    service:
      name: httpd
      state: started
  - name: config appache config port change
    lineinfile:
      path: /etc/httpd/conf/httpd.conf
      regexp: "Listen 80"
      line: "Listen 81"
  - name: add static config to servers
    template:
      src: index.html
      dest: /var/www/html/index.html
    notify: restart httpd







[root@main http-role]# cd templates/
[root@main templates]# cat ma
cat: ma: No such file or directory
[root@main templates]# ls
index.html
[root@main templates]# cat index.html
<html>
  <head>
    <title>Server Information</title>
  </head>
  <body>
    <h1> this is a demo for webserver hosted on {{ ansible_hostname }} and of os : {{ ansible_os_family }} !</h1>
</body>
</html>






====================================================================



upload : 

github repository

my content >> link my github repo to ansible galaxy 
private , public 


 ansible-galaxy install geerlingguy.apache
 1007  ls
 1008  cd /root/.ansible/roles/geerlingguy.apache
 1009  ls
 1010  cd ..
 1011  ls
 1012  cd ..
 1013  ls
 1014  cd roles/
 1015  ls
 1016  cp /root/raman/inv /root/.ansible/roles/geerlingguy.apache/
 1017  ls
 1018  cd geerlingguy.apache/
 1019  ls
 1020  mv inv ..
 1021  cd ..
 1022  ls
 1023  vi role.yml
 1024  vi role.yml
 1025  ansible-playbook -i inv role.yml
 1026  ls
 1027  cd geerlingguy.apache/
 1028  ls
 1029  cd tasks/
 1030  ls
 1031  cat main.yml


============================================





Tags:

[root@gagan-master ~]# cat first.yaml
---
- name: play1 for creating user on gagan-client machine
  hosts: gagan-client

  tasks:
    - name: 1 description for task1 for creating user
      user: name=gagandeep state=present
      when: ansible_distribution == "CentOS" and ansible_distribution_version == "7.7"
      register: user_out
      tags:
        - prod
        - dev

    - name: 2 false task
      debug:
        #msg="Print this msg only if user creation is successfull"
        var: user_out
      ignore_errors: true
      tags:
        - prod

    - name: 3 creating a file on next machine
      file:
        path: /tmp/gds
        state: touch
        mode: 1600
      when: ansible_distribution == "Redhat"

    - name: 4 description for task1 for creating user
      user: name=gagandeep1 state=present
      tags:
        - dev
[root@gagan-master ~]#

  433  ansible-playbook first.yaml --tags dev
  434  cat first.yaml
  435  ansible-playbook first.yaml --tags prod
  436  ansible-playbook first.yaml --skip-tags prod

 ansible-playbook first.yaml --start-at-task "3 creating a file on next machine"




==============================================================================================
```


