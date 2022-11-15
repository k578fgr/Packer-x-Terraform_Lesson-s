
























-------------------------
# Create the User Accounts Noted in /home/ansible/userlist.txt
Команда создаёт пользователей

ansible dbsystems -b -m user -a "name=consultant"
ansible dbsystems -b -m user -a "name=supervisor"


 # Place Key Files in the Correct Location, /home/$USER/.ssh/authorized_keys, on Hosts in dbsystems
 Поместить ssh ключи в authorized_keys src = source
 
 ansible dbsystems -b -m file -a "path=/home/consultant/.ssh state=directory owner=consultant group=consultant mode=0755"
 ansible dbsystems -b -m copy -a "src=/home/ansible/keys/consultant/authorized_keys dest=/home/consultant/.ssh/authorized_keys mode=0600 owner=supervisor group=supervisor"
 ansible dbsystems -b -m file -a "path=/home/supervisor/.ssh state=directory owner=supervisor group=supervisor mode=0755"
 ansible dbsystems -b -m copy -a "src=/home/ansible/keys/supervisor/authorized_keys dest=/home/supervisor/.ssh/authorized_keys mode=0600 owner=consultant group=consultant"



# Ensure auditd Is Enabled and Running on All Hosts
 ansible all -b -m service -a "name=auditd state=started enabled=yes