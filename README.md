#node-persist
###Super-easy persistent data structures in Node.js
This is still a work in progress. Send pull requests please.

##Install
1. Put 'persist.js' in your directory


2. 		var db = require('./persist');

##Basic
	//you must first call db.init or db.initSync
	db.init();
	
	//then start using it
	db.set('name','yourname');
	console.log(db.get('name'));
	
	var batman = {
		first: 'Bruce',
		last: 'Wayne',
		alias: 'Batman'
	};
	
	db.set('batman',batman);
	console.log(db.get('batman').alias);
	
##Options
You can pass init or initSync a hash options to customize the behavior of node-persist
	
	db.init({
			dir:'myDir', // The Directory to save documents
			interval:6000, // Saving interval, in milliseconds
			stringify: myStringifyFunction,
			parse: myParsingFunction,
			encoding: 'utf8',
			logging: false, //print db logs,
			isInterval: true // turn off for fine-grained control
	});
	
##Documentation
###get(key)
This function will get a key from your database, and return its value, or undefined if it is not present.
	
	db.get('name');
	db.get('obj').key1;
	db.get('arr')[42];


###set(key, value)
This function sets 'key' in your database to 'value'. It also sets a flag, notifying that 'key' has been changed and needs to be persisted in the next sweep.

	db.set('fibonacci',[0,1,1,2,3,5,8]);
	db.set(42,'the answer to life, the universe, and everything.')
	
	
##Fine-grained control
###persist(), persistSync()
These functions can be used to manually persist the database

		db.persist();
		db.persistSync();


###persistKey(key), persistKeySync(key)
These functions manually persist 'key' within the database

		db.set('name','myname');
		db.persistKey('name'); 
	