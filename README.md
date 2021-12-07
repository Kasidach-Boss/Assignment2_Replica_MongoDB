# Assignment2_Replica_MongoDB
for Internet Programming
# Command Line
# ติดตั้ง MongoDB
sudo apt update
sudo apt install mongodb 
sudo systemctl status mongodb 
mongo --version 

# ติดตั้ง Robo3t
sudo snap install robo3t-snap 

# ทำ replica 
mkdir replica_demo 
mkdir r1
mkdir r2
mkdir r3
mongod --replSet cmpos --logpath ./r1.log --dbpath ./r1 --port 27018 &
mongod --replSet cmpos --logpath ./r2.log --dbpath ./r2 --port 27019 &
mongod --replSet cmpos --logpath ./r3.log --dbpath ./r3 --port 27020 &
ls 
mongo --port 27018
config = {_id: "cmpos", members:[
{_id: 0, host: "localhost:27018"},
 {_id: 1, host: "localhost:27019"},
 {_id: 2, host: "localhost:27020"}]
}; 
rs.initiate(config);
rs.status();
exit

# ทดสอบ fialover
mongo --host cmpos/localhost:27018,localhost:27019,localhost:27020
use Assignment2
db.getCollection(‘courses’).find({})
ps -rf | grep mongod
