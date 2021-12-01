### DevOps 10
### HW_8.1. Введение в Ansible

---
Подготовка к выполнению

```
playbook|main⚡ ⇒ pwd                                    
/Users/nikitavinogradov/Documents/education/pyCharm/ansible_netology/08-ansible-01-base/playbook

playbook|main⚡ ⇒ ansible --version
ansible [core 2.11.6] 
  config file = None
  configured module search path = ['/Users/nikitavinogradov/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/Cellar/ansible/4.8.0/libexec/lib/python3.10/site-packages/ansible
  ansible collection location = /Users/nikitavinogradov/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.10.0 (default, Oct 22 2021, 13:39:57) [Clang 13.0.0 (clang-1300.0.29.3)]
  jinja version = 3.0.2
  libyaml = True
```

---
Основная часть </br>
1.</br>

```
playbook|main⚡ ⇒ ansible-playbook -i inventory/test.yml site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
[WARNING]: Platform darwin on host localhost is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could
change the meaning of that path. See https://docs.ansible.com/ansible-core/2.11/reference_appendices/interpreter_discovery.html for more information.
ok: [localhost]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "MacOSX"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP *******************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
2.</br>
В файле ```./group_vars/all/examp.yml``` изменил значение для параметра ```some_fact``` на ```"all default fact"```. Результат вывода:

```
playbook|main⚡ ⇒ ansible-playbook -i inventory/test.yml site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
[WARNING]: Platform darwin on host localhost is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could
change the meaning of that path. See https://docs.ansible.com/ansible-core/2.11/reference_appendices/interpreter_discovery.html for more information.
ok: [localhost]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "MacOSX"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}

PLAY RECAP *******************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
3.</br>
Использую *docker*

4.</br>

```
playbook|main⚡ ⇒ docker ps -a
CONTAINER ID   IMAGE                   COMMAND                CREATED      STATUS          PORTS     NAMES
150d7187b161   arm64v8/ubuntu:latest   "sleep 600000000000"   3 days ago   Up 40 seconds             ubuntu
d95efe99742c   arm64v8/centos:7        "sleep 600000000000"   3 days ago   Up 38 seconds             centos7
```

``` 
playbook|main⚡ ⇒ ansible-playbook -i inventory/prod.yml  site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}

PLAY RECAP *******************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
```
Для контейнера ```centos7``` значение ```some_fact``` приняло значение ```el```</br>
Для контейнера ```ubuntu``` значение ```some_fact``` приняло значение ```deb```</br>

5.</br>
Изменил значения для ```deb/examp.yml``` и ```el/examp.yml``` на требуемые.

6.</br>

``` 
playbook|main⚡ ⇒ ansible-playbook -i inventory/prod.yml  site.yml 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *******************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   


```
7.</br>

``` 
playbook|main⚡ ⇒ ansible-vault encrypt ./group_vars/deb/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
playbook|main⚡ ⇒ ansible-vault encrypt ./group_vars/el/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
```
8.</br>

``` 
playbook|main⚡ ⇒ ansible-playbook -i inventory/prod.yml  --ask-vault-password site.yml 
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *******************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
9.</br>

``` 
playbook|main⚡ ⇒ ansible-doc -t connection -l > ./ansible_doc_connection_plugins.txt
[WARNING]: Collection frr.frr does not support Ansible version 2.11.6
[WARNING]: Collection ibm.qradar does not support Ansible version 2.11.6
[WARNING]: Collection splunk.es does not support Ansible version 2.11.6
```

10.</br>
Содержимое файла ```prod.yml```:

``` 
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker
  inside:
    hosts:
      localhost:
        ansible_connection: local
```
``` 
playbook|main⚡ ⇒ less ansible_doc_connection_plugins.txt  
```
Результат вывода:

``` 
ansible.netcommon.httpapi      Use httpapi to run command on network applia...
ansible.netcommon.libssh       (Tech preview) Run tasks using libssh for ss...
ansible.netcommon.napalm       Provides persistent connection using NAPALM 
ansible.netcommon.netconf      Provides a persistent connection using the n...
ansible.netcommon.network_cli  Use network_cli to run command on network ap...
ansible.netcommon.persistent   Use a persistent unix socket for connection 
community.aws.aws_ssm          execute via AWS Systems Manager             
community.docker.docker        Run tasks in docker containers              
community.docker.docker_api    Run tasks in docker containers              
community.docker.nsenter       execute on host running controller container
community.general.chroot       Interact with local chroot                  
community.general.funcd        Use funcd to connect to target              
community.general.iocage       Run tasks in iocage jails                   
community.general.jail         Run tasks in jails                          
community.general.lxc          Run tasks in lxc containers via lxc python l...
community.general.lxd          Run tasks in lxc containers via lxc CLI     
community.general.qubes        Interact with an existing QubesOS AppVM     
community.general.saltstack    Allow ansible to piggyback on salt minions  
community.general.zone         Run tasks in a zone instance                
community.kubernetes.kubectl   Execute tasks in pods running on Kubernetes 
community.libvirt.libvirt_lxc  Run tasks in lxc containers via libvirt     
community.libvirt.libvirt_qemu Run tasks on libvirt/qemu virtual machines  
community.okd.oc               Execute tasks in pods running on OpenShift  
community.vmware.vmware_tools  Execute tasks inside a VM via VMware Tools  
containers.podman.buildah      Interact with an existing buildah container 
containers.podman.podman       Interact with an existing podman container  
kubernetes.core.kubectl        Execute tasks in pods running on Kubernetes 
local                          execute on controller                       
paramiko_ssh                   Run tasks via python ssh (paramiko)
psrp                           Run tasks over Microsoft PowerShell Remoting...
ssh                            connect via ssh client binary               
winrm                          Run tasks over Microsoft's WinRM  
```

11.</br>

``` 
playbook|main⚡ ⇒ ansible-playbook -i inventory/prod.yml  --ask-vault-password site.yml 
Vault password: 

PLAY [Print os facts] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
[WARNING]: Platform darwin on host localhost is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could
change the meaning of that path. See https://docs.ansible.com/ansible-core/2.11/reference_appendices/interpreter_discovery.html for more information.
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "MacOSX"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *******************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```


