### GPS Tracker using Navtrack

1. download zip of mongosh from mongodb website. extract the file and paste in mongodb installed location.
2. now mongosh exe file location would be like C:\Program Files\MongoDB\mongosh\bin.
3. add system environment variable as mongosh to C:\Program Files\MongoDB\mongosh\bin\ location.
4. restart your machine or go to C:\Program Files\MongoDB\mongosh\bin in command prompt.
5. run command steps by steps.
   ```sh
    show dbs
   ```sn
6. switch to navtrack db using below command
> use navtrack
7. show list of collections
> show collections
8. to find any device collection data
> db.deviceConnections.find()
9. switch to admin database
> use admin
> db.getUsers()
10. create user in admin db for navtarck database
> db.createUser({
  user: "gpsadmin",
  pwd: "pcsgps123",
  roles: [
    { role: "readWrite", db: "navtrack" }
  ]
})

10. edit mongod.conf file for enable security

#security

security:
  authorization: "enabled"

1. change connection string for navtrack exe and Asset Infinity Webapi
1. Add a asset to start getting location. 
  
{{url}}/api/gps/assets
{
    "name": "teltonika",
    "deviceTypeId": "1",
    "serialNumber": "352016701673261"
}
