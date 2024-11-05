### GPS Tracker using Navtrack

1. download zip of mongosh from mongodb website. extract the file and paste in mongodb installed location.
2. now mongosh exe file location would be like C:\Program Files\MongoDB\mongosh\bin.
3. add system environment variable as mongosh to C:\Program Files\MongoDB\mongosh\bin\ location.
4. restart your machine or go to C:\Program Files\MongoDB\mongosh\bin in command prompt.
5. run command steps by steps.
```sh
 show dbs
```
6. switch to navtrack db using below command
```sh
 use navtrack
```
7. show list of collections
```sh
show collections
```
9. to find any device collection data
```sh
db.deviceConnections.find()
```
9. switch to admin database
```sh
use admin
db.getUsers()
```
10. create user in admin db for navtarck database
```sh
 db.createUser({
  user: "gpsadmin",
  pwd: "pcsgps123",
  roles: [
    { role: "readWrite", db: "navtrack" }
  ]
})
```
10. edit mongod.conf file for enable security

#security

security:
  authorization: "enabled"

1. change connection string for navtrack exe and Webapi appsettings
1. Add a asset to start getting location. 
  
{{url}}/api/gps/assets
{
    "name": "teltonika",
    "deviceTypeId": "1",
    "serialNumber": "352016701673261"
}
