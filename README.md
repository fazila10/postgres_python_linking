# postgres_python_linking
**Postgres:**
```
1.docker pull postgres	 //pulls latest image

2.docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres 	//run the image(it downloads if not present)

3.docker exec -it some-postgres bash 	//connect to the container //opens in root

4.su postgres				//change user to postgres

5.psql					//run sql

6.\conninfo

7.\q					//to quit
```
**Networking postgres and ubuntu:**
```
1.docker network ls   							//displays all the network which is present

2.docker network create --driver driver_name network_name		//creates a new network
  ->docker network create --driver bridge new_network

Connect a new container:			//using bridge
3.docker run -it --network=new_network ubuntu:latest /bin/bash		//creates ubuntu in the network we created

4.docker run -it --network=new_network --name faz_postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres	//creates postgres in the network we created

5.docker inspect new_network 			//inspect the network to check if containers are attached
						// conatiners will be attached to network.
```
**Connect a running container to a newwork:**
```
docker network connect network-name container-name
```

**Connecting jupyter to postgres**
```
import psycopg2  
import pprint

conn = psycopg2.connect("postgres://postgres:mysecretpassword@172.17.0.3:5432/postgres")
```

**Working SQL commands:**
```
!pip install ipython-sql
%load_ext sql
%sql sqlite://
```

**CREATE TABLE AND INSERTING:**
```
%%sql
CREATE TABLE EMP(firstname varchar(50),lastname varchar(50));
INSERT INTO EMP VALUES('tom','Mitchell');
INSERT INTO EMP VALUES('jack','ryan');
INSERT INTO EMP VALUES('kim','taehyung');
INSERT INTO EMP VALUES('kim','namjoon');

%sql SELECT * from EMP
```

**ERROR:**
```
 docker inspect container_name  //To find ip address 

 \conninfo   //To find user name  
```
**links:**

1.Networking postgres and ubuntu:https://www.geeksforgeeks.org/creating-a-network-in-docker-and-connecting-a-container-to-that-network/#:~:text=%20%20%201%20Step%201%3A%20.%20In,next%20step%20connect%20the%20container%20to...%20More%20

2.Connecting jupyter to postgres:https://medium.com/analytics-vidhya/postgresql-integration-with-jupyter-notebook-deb97579a38d

3.CREATE TABLE AND INSERTING:https://www.datacamp.com/community/tutorials/sql-interface-within-jupyterlab
