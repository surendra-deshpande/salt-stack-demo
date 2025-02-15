# salt-stack-demo
Setup salt stack using docker compose on local.

Before you start experimenting.
Create private key and public key for minion and master and paste it in respective keys folder. 
https://stackoverflow.com/questions/25138290/how-can-i-generate-a-salt-minion-key-pair-using-openssl

Use docker-compose to setup salt master with minions. 
```docker compose up```

Now exec into salt-master and execute the following command to check minions connected to master. 
``` docker ps``` this will give the list of running containers. 
pick the salt master container id and exec into it. 
``` docker exec it <salt-master-container-id> bash```
once into the salt master container - execute the following command to check list of minion ids connected to master. 
```salt-key```

Now scale the minions from another terminal using the below command. 
```docker compose scale minion1=3```

Now again exec into master container and verify if you see 3 minions connected. 
```salt-key``` Execute this command in salt master container.

Now run ```salt '*' test.ping``` from salt master which will execute on all the minions

Now scale down the minions using the following command. (This will scale down 3 minions to 1)
```docker compose scale minion1=1```

Run the follwing command on a different terminal to check if only 2 containers are running ( 1 is the salt master, 1 is the minion)
``` docker ps``` this will give the list of running containers. 

Run the following command on master to clean up stale minions that are not active. 
```salt-run manage.down removekeys=True```