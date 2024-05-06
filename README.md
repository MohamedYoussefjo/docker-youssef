---Manuell d’installation de hadoop sur 
un cluster Docker- ---
1-Installation de Docker : 
 -sudo apt update
 -sudo apt upgrade
 -sudo apt install docker.io
 -sudo apt install docker-compose
 -sudo apt install docker-ce
Verification de l’installation par (sudo docker run hello-world)
2-TéLéchargement de docker-hadoop 
Git clone https://github.com/gimsaito1/docker-youssef.git
Cd /home/vboxuser ou cd 
Aprés : unzip docker-hadoop.zip (il faut d’abord installer zip : sudo apt 
install zip)
3-Création de l’image de base pour tous les containers :
Sudo build –t bde2020/hadoop-base:2.0.0-hadoop3.2.1-javabyyou
/home/vboxuser/docker-haddop/base/
4-On va creer tous les containers maintenant :
Sudo docker-compose up –d (Pour ne pas voir le processus de 
configuration et pas perdre le controle du terminal)
5-Verification si les containers sont bien crées :
Sudo docker ps
Normalement on doit trouver containers avec les nom datanode1 ,2 ,3 
,resourcemanager ,Historyserver , namenode ,nodemanager 
Et aussi on peut verifier avec localhost:9870 dans votre navigateur 
6-copie du fichier purchases.txt du Downloads vers hdfs 
Hdfs dfs –mkdir /input
Hdfs dfs –copyFromLocal ~/Downloads/purchases.txt /input
7-on va entrer maintenant dans le container namenode 
Sudo docker exec –it namenode bash ou bien Sudo docker exec –it 
<idofcontainer> bash 
9-On peut maintenat execute notre jar file
Il faut s’assurer bien que les fichier Mapper.py et Reducer.py sont tous 
existants dans le répertoire “mr” de tous les containers 
Hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.2.1.jar -mapper /mr/Mapper.py -reducer /mr/Reducer.py -file 
/mr/Mapper.py -file /mr/Reducer.py -input /input -output /joboutput
Lorsque on a finit notre travail on peut fermer les containers avec 
Sudo Docker-compose dow
