
#MongDB


#STEP 1 - Installation

Having run thru a few installation cycles in Windows and Debian. For Windows, it is pretty straight forward, everything starts from msi installation. But it is a little bit tricky for Ubuntu and Debian and I personally suggest you to follow the updated guidelines stated in MongoDB official website: https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/

It is the most reliable source thus far.



#STEP 2 - Configuration

To start mongod service, MongoDB reserves 3GB space for writing into memory before the actual commit. I strongly encourage you to leave this option open in production. However, if you have limited space in development environment, you can turn off this feature by changing Mongod's configuration at /etc/mongod.conf 

storage:
  dbPath: /var/lib/mongodb 	<=== default data/db storage in configuration file
  journal: 
    enabled: false			<=== if journal's enabled is true, 3GB will be reserved. if you do not want to reserve 3GB, please use false.


# STEP 3 - Start and Stop MongoD in Ubuntu or Debian

To start MongoDB, we need to open two shells. One is for MongoDB server listener, another one is for client connection. After started server listener service, we will use client shell to test the connectivity.

Command to start MongoDB server listener:
	mongod --config /etc/mongod.conf

Command to stop MongoDB's service:
	sudo service mongod stop


# STEP 4 - Import Test Database to MongoDB

You can download the test database file from http://media.mongodb.org/zips.json. We will use the json file for test import.

Command to import MongoDB database (open a new shell in your distro):
	mongoimport --db [DATABASE_NAME] --collection zips --drop --file [YOUR ZIPS.JSON FILE LOCATION]

	Example command: mongoimport --db test --collection zips --drop --file /home/xineloper/Downloads/zips.json

The import will only take a few seconds to complete, it will tell you number of imported records once it is complete


# STEP 5 - Test Client Connectivity

To test MongoDB server connection, you need to start mongo client using the following shell command:

	mongo

Once it is connected to MongoDB server, it will print the version of your installed MongoDB and database that you connected to. If you have test database imported, you can try to find record using the following command query:

	db.zips.findOne()

You will see a json type of output after executed the command query. To disconnect client from server, use Ctrl-C or exit command.

Good luck!
