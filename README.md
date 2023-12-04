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


