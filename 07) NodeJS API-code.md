1. Initiate project using : npm init to create a package.json file 

    - Go to package.json and add following scripts : 
    - “start”:”npm src/server.js”,
    - “dev”:”nodemon src/server.js” 

2. Install following dependencies : cors, dotenv, express, mongoose, nodemon

3. Create the folder structure as : 

src > db > conn.js
    > models > batsmen.js
    > routers > men.js
    > app.js


4. Add following code to **server.js** : 

const express=require("express");
const server=express();
const cors=require("cors");
server.use(cors());
const port=process.env.PORT||3000;
require("./db/conn");
const MensRanking=require("./models/batsmen");
const router=require("./routers/men");
server.use(express.json());
server.use(router);
server.listen(port,()=>{
    console.log(`Connection is successful to the webserver`);
})


5. Now I will open mongoDb cloud and signin with email. 

    - Then create a new project, give it a name, and then click create the database. 

    - Select the free services, your region, Cluster0 (default) and then create. Then it asks me to create a username and password and gives a default suggestion. 
    
    - Copy this password and paste it in the .env file we have created in the root of our project. Then i will click on create user
    
    - Then it asks me to Add entries to the IP access list. We add IP : 0.0.0.0/0 and then finish and close 

    - Then we connect our cluster. It gives various options to connect my database. 
    
    - Select VS code. It will provide a connection string like : 
    mongodb+srv://swpnilpndey:<password>@cluster0.meiz4ta.mongodb.net/test

    - We need to replace <password> with the password we wrote in .env file when we were creating the user

    - Add the string in .env file created in root : 

    MONGO_URI=mongodb+srv://swpnilpndey:9iuYVQSutMKB8SXr@cluster0.oi36zqn.mongodb.net/test


6. Add following code to **conn.js** to create the connection of web server to database : 

const mongoose=require("mongoose");
require("dotenv").config();
mongoose.connect(process.env.MONGO_URI,{
    useNewUrlParser:true,
   }).then(()=>{
    console.log(`Connection to database is successful`);
}).catch((error)=>{
    console.log(error);
})


7. Add following code to **batsmen.js** to create the database schema (what type of data will be there) : 

const mongoose=require("mongoose");
const menSchema=new mongoose.Schema({
    ranking:{
        type:Number,
        required:true,
        unique:true
    },
    name:{
        type:String,
        required:true,
    },
    country:{
        type:String,
        required:true,
    },
    points:{
        type:Number,
        required:true,
    },
    event:{
        type:String,
        default:"T20"
    },
})

const MensRanking=new mongoose.model("MenRanking",menSchema);
module.exports=MensRanking;



8. Now add the following code in men.js : 

const express=require("express");
const router=new express.Router();
const MensRanking=require("../models/batsmen");

router.post("/",async(req,res)=> {
    try {
        const addingRecords=new MensRanking(req.body);
        const saveRecords=await addingRecords.save();
        res.status(201).send(saveRecords);
    } catch (error) {
        res.status(400).send(error);        
    }
})
router.get("/",async(req,res)=> {
    try {
        const getMens= await MensRanking.find({}).sort({"ranking":1}); // to recieve sorted data
        res.send(getMens);             
    } catch (error) {
        res.status(400).send(error);        
    }
})
router.get("/:id",async(req,res)=> {
    try {
        const _id=req.params.id;
        const getMen= await MensRanking.findById({_id:_id});
        res.send(getMen);             
    } catch (error) {
        res.status(400).send(error);        
    }
})
router.patch("/:id",async(req,res)=> {
    try {
        const _id=req.params.id;
        const getMen= await MensRanking.findByIdAndUpdate({_id:_id},req.body,{new:true});
        res.send(getMen);             
    } catch (error) {
        res.status(500).send(error);        
    }
})
router.delete("/:id",async(req,res)=> {
    try {
        const _id=req.params.id;
        const getMen= await MensRanking.findByIdAndDelete({_id:_id});
        res.send(getMen);             
    } catch (error) {
        res.status(500).send(error);        
    }
})

module.exports=router; 



9. Now open POSTMAN and create a new collection - Batsmen T20

After that, I will add a new request to this collection and give it a name - create Batsmen

Then I will use the POST method on it on API URL 

Now, I will create a JSON file in chat gpt from whatever the data format is there to be pushed 

After that I will copy the first data entry and then in POSTMAN, I will goto Body tab below the API address and in the Body tab, select raw and change Text to JSON. Then paste the entries from chat gpt : 
{
    "ranking": 1,
    "name": "Suryakumar Yadav",
    "country": "INDIA",
    "points": 906
  }


This way, we create a new data entry in database from POST request in POSTMAN. 

Now, I will send the data from POSTMAN

This way I will send the data from POSTMAN for all 10 batsmen, one by one 

### I can change a data field using PATCH method

For this, I will go to API URL/:id (ID is visible in Mongdb cloud) in POSTMAN and use patch request. 

For example, I want to change the points of Rank 1 from 907 to 910, I will write : 
{
    "points": 910
}
Then I click on the send button in POSTMAN and the data is updated. 


### Similarly I can delete data as well using POSTMAN by simply going to API URL/:ID and using DELETE method

