# node-express-mongoose-starter

# Deploy Express app to Vercel

আমরা আজকে জানব Vercel এ আমাদের ExpressJS app deploy করার সময় কি কি বিষয় খেয়াল রাখতে হবে। 

# ExpressJS

 

- [ ]  `vercel --prod` কমান্ড দিয়ে deploy করলে deploy করা server API link চেঞ্জ হয় না , বার বার deploy করলেও link same থাকে।
- [ ]  Vercel এর dashboard ⇒ project settings এ যেয়ে Domain এর নিজে থাকা Link টা ব্যবহার করতে হবে, terminal এ দেয়া লিংকটা অনেক সময় change হয়ে যায়, প্রতিবার deploy করলে
- [ ]  .env ফাইলে থাকা variable গুলি index.js এ ব্যবহার করার সময় একই বানান ব্যবহার করতে হবে। এটা Case Sensitive.
- [ ]  `await client.connect();` এবং `await client.close()` এই লাইন গুলি commented থাকতে হবে
- [ ]  package.json এ “script” এর { } মধ্যে “start”: “node index.js” থাকতেই হবে for example

```json
{
	"name": "example-server",
	"version": "1.0.0",
	"description": "",
	"main": "index.js",
	"scripts": {
		"start": "node index.js",
		"dev": "nodemon index.js",
		"test": "echo \"Error: no test specified\" && exit 1"
	},
	"keywords": [],
	"author": "",
	"license": "ISC",
	"dependencies": {
		"cors": "^2.8.5",
		"dotenv": "^16.3.1",
		"express": "^4.18.2",
		"mongodb": "^6.1.0"
	}
}
```

- [ ]  vercel.json file থাকতে হবে যেখানে আপনার index.js file টা থাকবে, ঠিক তার same folder এ

```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "index.js"
    }
  ]
}
```

# MongoDB

- [ ]  Network Access Menu তে সবগুলি IP address এ access দিতে হবে। অর্থাৎ 0.0.0.0/0 IP address allow করতে হবে
- [ ]  Database Access Menu তে থাকা database username এবং password ঠিকঠাক ব্যবহার করা হচ্ছে কিনা Ensure করতে হবে। Generate Secure Password এ click করার পর Password Copy করে **অবশ্যই নিচে Scroll করে Update User [সবুজ] button টায় click করতে হবে**
- [ ]  Database Menu তে থাকা Connect button ⇒ Drivers এ click করে আপনার Mongo URI কপি করতে হবে।
- [ ]  ExpressJS এ Mongo URI ব্যবহার করার সময় এটা template string আকারে রাখতে হবে এবং এতে env variable এ থাকা database username ও password ঠিকঠাক ভাবে process.env দিয়ে access করতে হবে, এই ব্যাপার বিস্তারিত ExpressJS section এ বলা হল।
