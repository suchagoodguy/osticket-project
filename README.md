# osticket-project
HA osTicket (HAproxy, nginx, Percona XtraDB Cluster)

To start:

vagrant up

ansible-playbook -i hosts main.yml

Then open in browser:

http://192.168.70.11

For DB setup use:

host 127.0.0.1

DB name osticket

user root

password mysqlgfhjkm

After successful initial setup run as root at both web1 and web2:

/vagrant/remove_setup_scripts
