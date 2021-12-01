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

