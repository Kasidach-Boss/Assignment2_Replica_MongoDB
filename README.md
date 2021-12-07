# Assignment2_Replica_MongoDB
for Internet Programming
# Command Line
# ติดตั้ง MongoDB
sudo apt update <br/>
sudo apt install mongodb <br/>
sudo systemctl status mongodb <br/>
mongo --version <br/>

# ติดตั้ง Robo3t
sudo snap install robo3t-snap <br/>

# ทำ replica 
mkdir replica_demo <br/>
mkdir r1<br/>
mkdir r2<br/>
mkdir r3<br/>
mongod --replSet cmpos --logpath ./r1.log --dbpath ./r1 --port 27018 &<br/>
mongod --replSet cmpos --logpath ./r2.log --dbpath ./r2 --port 27019 &<br/>
mongod --replSet cmpos --logpath ./r3.log --dbpath ./r3 --port 27020 &<br/>
ls <br/>
mongo --port 27018<br/>
config = {_id: "cmpos", members:[ <br/>
{_id: 0, host: "localhost:27018"},<br/>
 {_id: 1, host: "localhost:27019"},<br/>
 {_id: 2, host: "localhost:27020"}]<br/>
}; <br/>
rs.initiate(config);<br/>
rs.status();<br/>
exit<br/>

# ทดสอบ failover
mongo --host cmpos/localhost:27018,localhost:27019,localhost:27020<br/>
use Assignment2<br/>
db.getCollection(‘courses’).find({})<br/>
ps -rf | grep mongod<br/>

Ref<br>
https://docs.mongodb.com/manual/replication/ <br>

