# Tutos-Replication-Master-Slave
Ce tuto nous montre comment faire la replication entre deux bases des données master slave et master master . nous allons commencé par master slave, pour ce faire il faut avoir deux instances bien créé depuis amazon ec2 linux 2 et le ssh avec mobaxterm .Ensuite, nous allons configurer la réplication entre le serveur maître et le serveur esclave en modifiant les fichiers de configuration MySQL et en redémarrant les instances. Suivez attentivement les étapes pour vous assurer que la réplication se déroule correctement et que les données sont synchronisées entre les deux bases de données.
Etape pour l'installation de Mariadb;

sudo yum install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
