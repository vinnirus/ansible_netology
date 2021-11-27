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
playbook|main⚡ansible-playbook -i test.yml ./site.yml                                                     kk
[WARNING]: Unable to parse /Users/nikitavinogradov/Documents/education/pyCharm/ansible_netology/08-ansible-01-base/playbook/test.yml as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [Print os facts] ********************************************************************************************************************************************************
skipping: no hosts matched

PLAY RECAP *******************************************************************************************************************************************************************
```

Любые попытки внести изменения в ```ansible.cfg``` и в файл ```hosts```  к успеху не привели. 
Каким образом можно решить данную проблему?

2.</br>


