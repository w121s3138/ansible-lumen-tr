```
practise server :


main pr : 54.166.188.236

m1: 54.156.38.7

m2: 54.152.71.205

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
