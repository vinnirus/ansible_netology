### DevOps 10
### HW_8.2 Работа с Playbook

Основная часть </br>
1.</br>

```
playbook|main⚡ ⇒ ansible-playbook -v -i inventory/prod.yml -K site.yml
Using /etc/ansible/ansible.cfg as config file
BECOME password: 

PLAY [Install Java] **********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]

TASK [Set facts for Java 17 vars] ********************************************************************************************************************************************
ok: [ubuntu] => {"ansible_facts": {"java_home": "/opt/jdk/17"}, "changed": false}

TASK [Upload .tar file containing binaries from local storage] ***************************************************************************************************************
ok: [ubuntu] => {"attempts": 1, "changed": false, "checksum": "b76bc0cb631e1a0901ac9c455f6b1d0a516f16f4", "dest": "/tmp/jdk-17.tar", "gid": 1001, "group": "nikitavinogradov", "mode": "0664", "owner": "nikitavinogradov", "path": "/tmp/jdk-17.tar", "size": 317378560, "state": "file", "uid": 1001}

TASK [Ensure installation dir exists] ****************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "gid": 0, "group": "root", "mode": "0755", "owner": "root", "path": "/opt/jdk/17", "size": 4096, "state": "directory", "uid": 0}

TASK [Extract java in the installation directory] ****************************************************************************************************************************
skipping: [ubuntu] => {"changed": false, "msg": "skipped, since /opt/jdk/17/bin/java exists"}

TASK [Export environment variables] ******************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "checksum": "0d8082fb06400868354524f72c727c234657e4a9", "dest": "/etc/profile.d/jdk.sh", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/etc/profile.d/jdk.sh", "size": 180, "state": "file", "uid": 0}

PLAY [Install Elasticsearch] *************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]

TASK [Upload tar.gz Elasticsearch from remote URL] ***************************************************************************************************************************
ok: [ubuntu] => {"attempts": 1, "changed": false, "dest": "/tmp/elasticsearch-7.16.1-linux-aarch64.tar.gz", "elapsed": 0, "gid": 1001, "group": "nikitavinogradov", "mode": "0755", "msg": "HTTP Error 304: Not Modified", "owner": "nikitavinogradov", "size": 339137223, "state": "file", "status_code": 304, "uid": 1001, "url": "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.16.1-linux-aarch64.tar.gz"}

TASK [Create directory for Elasticsearch] ************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "gid": 0, "group": "root", "mode": "0755", "owner": "root", "path": "/opt/elastic/7.16.1", "size": 4096, "state": "directory", "uid": 0}

TASK [Extract Elasticsearch in the installation directory] *******************************************************************************************************************
skipping: [ubuntu] => {"changed": false, "msg": "skipped, since /opt/elastic/7.16.1/bin/elasticsearch exists"}

TASK [Set environment Elastic] ***********************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "checksum": "4bfae26685ed6309b095a47a6f0012709f29d32d", "dest": "/etc/profile.d/elk.sh", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/etc/profile.d/elk.sh", "size": 184, "state": "file", "uid": 0}

PLAY [Install Kibana] ********************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************
ok: [ubuntu]

TASK [Upload tar.gz Kibana from remote URL] **********************************************************************************************************************************
ok: [ubuntu] => {"attempts": 1, "changed": false, "dest": "/tmp/kibana-7.16.1-linux-aarch64.tar.gz", "elapsed": 0, "gid": 1001, "group": "nikitavinogradov", "mode": "0755", "msg": "HTTP Error 304: Not Modified", "owner": "nikitavinogradov", "size": 294086436, "state": "file", "status_code": 304, "uid": 1001, "url": "https://artifacts.elastic.co/downloads/kibana/kibana-7.16.1-linux-aarch64.tar.gz"}

TASK [Create directory for Kibana] *******************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "gid": 0, "group": "root", "mode": "0755", "owner": "root", "path": "/opt/kibana/7.16.1", "size": 4096, "state": "directory", "uid": 0}

TASK [Extract Kibana in the installation directory] **************************************************************************************************************************
skipping: [ubuntu] => {"changed": false, "msg": "skipped, since /opt/kibana/7.16.1/bin/kibana exists"}

TASK [Set environment Kibana] ************************************************************************************************************************************************
ok: [ubuntu] => {"changed": false, "checksum": "0d92fec12846ce68cd8c09543a0eb9edd2cf9322", "dest": "/etc/profile.d/kibana.sh", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/etc/profile.d/kibana.sh", "size": 191, "state": "file", "uid": 0}

PLAY RECAP *******************************************************************************************************************************************************************
ubuntu                     : ok=13   changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0   

playbook|main⚡ ⇒   

```
