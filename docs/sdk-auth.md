# Customer registration

Skycharge broker has an authentication mechanism for all remote clients, 
so all customers who need access to the Skycharge cloud SDK have to be
registered explicitly and manually (there is no way to register a customer
from the Skycharge web cloud unfortunately).

## Procedure

1) A customer has to create an account on the [Skycharge Cloud](https://cloud.skycharge.de) with common procedure through the email/google acc/etc.

2) Once a customer creates an account the Skycharge Cloud, admin requests from the customer 'user-uuid' (taken from the skycharge.conf or generated) and email i.e:
   
   - email: demo@demo.demo
   - user-uuid: 00000000-0000-0000-0000-000000000000

1) Connect to the skybroker host: ssh -i skycharge-amazon.pem admin@install.skycharge.de

2) Start MongoDB client on the skybroker host:
```shel
mongosh mongodb://172.31.45.75/skycharge_db
```
The IP 172.311.45.75 is the IP of the other EC2 instance hosting skycharge-mongodb. 

5) Find ObjectId by the customer email:
```bash
db.users.find({ email: 'demo@demo.demo'}, {_id:true})
```
expected answer:
```json
[ { _id: ObjectId("61a8811b391ad3e1a3755253") } ]
```

Check user data with the _id
```sql
db.users.find({_id: ObjectId("61a8811b391ad3e1a3755253")})
```

6) Set ObjectId of the customer user to the userUUID collection searching by the 'user-uuid':
```sql
db.userUUIDS.updateOne({userUUID: `00000000-0000-0000-0000-000000000000`}, { $set: {userId: ObjectId(`61a8811b391ad3e1a3755253`)} })
```
expected response:
```json
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
The client should have access to SDK after successful updating the database.
To leave mongo shell:
```bash
quit()
```
or use the Ctrl-C shortcut.



## Test
```bash
curl 'https://api.skycharge.de/v1/devs-list?user-uuid=00000000-0000-0000-0000-000000000000'
```


## Usefull mongodb commands

Print a list of all collections for current database:
```sql
db.getCollectionNames()
```

List of users:
```sql
db.users.find()
db.users.find({_id: 'ObjectId("624bedba6bc6347b91b74886")'})
```

List device config, asociated user, state etc
```sql
db.chargers.find({deviceId: 'e33fc13d-7215-4b0d-b8c5-2ed7b10b3547’})
```

<!--
Dirty notes to be formated and checked

List matches:
```sql
 db.userUUIDS.find()
```

after id object from email
```sql
db.userUUIDS.find({_id: `ObjectId("624bedba6bc6347b91b74886")`})
```


after userUUID
 ```sql
db.userUUIDS.find({userUUID: `44c02bdb-5f33-4237-bb6f-90bca4060a4b`})
```


db.chargers.find({deviceId: 'c79cd29d-5fd9-447e-a291-38fe5ef490a7'})

db.chargers.find({name: 'arkspick'})
db.chargers.find({name: 'intsmsee'})

-->