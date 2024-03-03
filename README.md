# Tutos-Replication-Master-Slave
Ce tuto nous montre comment faire la replication entre deux bases des données master slave et master master . nous allons commencé par master slave, pour ce faire il faut avoir deux instances bien créé depuis amazon ec2 linux 2 et le ssh avec mobaxterm .Ensuite, nous allons configurer la réplication entre le serveur maître et le serveur esclave en modifiant les fichiers de configuration MySQL et en redémarrant les instances. Suivez attentivement les étapes pour vous assurer que la réplication se déroule correctement et que les données sont synchronisées entre les deux bases de données.

Etape pour l'installation de Mariadb;

```bash
sudo yum install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Secure MariaDB installation;
```bash
sudo mysql_secure_installation
```
Ouvrez le fichier de configuration ;

```bash
sudo nano /etc/my.cnf.d/server.cnf
```
Vous devrez avoir cette configuration;


![image](https://github.com/AWS-Re-Start-RDC-KINSHASA-1/Tutos-Replication-Master-Slave-and-Master-Master/assets/114914329/d02471b0-39f9-4a8e-bf48-40ace7e2d5c4)

Ensuite rédemarer mariadb;

```bash
sudo systemctl restart mariadb
```

Ensuite créer un user et donner les privillèges;

```bash
CREATE USER 'replication_user'@'%' IDENTIFIED BY 'your_password';
GRANT REPLICATION SLAVE ON *.* TO 'replication_user'@'%';
FLUSH PRIVILEGES;
```

NB: Remplace 'replication_user' par ton nom et 'your_password' par ton mot de passe choisi. Voici un exemple :


![image](https://github.com/AWS-Re-Start-RDC-KINSHASA-1/Tutos-Replication-Master-Slave-and-Master-Master/assets/114914329/ee150c7f-b6b2-46b6-84b0-b494e9c1fa1f)


Ensuite, vérifiez le statut du master;

```bash
SHOW MASTER STATUS;
```

![image](https://github.com/AWS-Re-Start-RDC-KINSHASA-1/Tutos-Replication-Master-Slave-and-Master-Master/assets/114914329/a8ed6ee0-f3fe-4658-aa64-b1fff77dde70)


Configurer la réplication avec la seconde instances;


```bash
CHANGE MASTER TO
   MASTER_HOST='second_instance_ip',
   MASTER_USER='repl',
   MASTER_PASSWORD='your_password',
   MASTER_LOG_FILE='second_master_log_file',
   MASTER_LOG_POS=second_master_log_pos;
```

NB: Pour la section MASTER_HOST : mettre l'adresse IP du maître, MASTER_USER : mettre le nom de l'utilisateur créé, MASTER_PASSWORD : mettre le mot de passe créé pour l'utilisateur, MASTER_PASSWORD : mettre le fichier journal et le MASTER_LOG_POS : mettre la position.

![image](https://github.com/AWS-Re-Start-RDC-KINSHASA-1/Tutos-Replication-Master-Slave-and-Master-Master/assets/114914329/66ff21de-192e-416d-a1ba-9105a3cf1be4)


mysql-bin.000009 : MASTER_LOG_FILE
783: MASTER_LOG_POS




