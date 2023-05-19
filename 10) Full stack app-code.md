1. Initialize project using npm using : npm init, main:app.js is to be set

2. Install dependencies as : npm i express mongoose hbs bcryptjs cookie-parser dotenv jsonwebtoken nodemon

3. Add following scripts in package.json : 

"dev": "nodemon src/app.js -e js, hbs",
"start": "node src/app.js"

4. Create following folder structure : 

![Folder structure for fullstack app](/images/full_stack_app_folders.PNG)


5. styles.css inside public/css will have all the CSS based on respective class/IDs/element

6. forMain inside public folder has all those images, gifs, audios, videos that our front end will use 

7. conn.js inside src/db has following code : 

**It is used to connect to the mongoDB database**

const mongoose=require("mongoose");
require("dotenv").config();
mongoose.connect(process.env.MONGO_URI,{
    useNewUrlParser:true,
    }).then(()=>{
    console.log("Connection to database is successful");
}).catch((e)=>{
    console.log(e);
})


8. auth.js inside src/middleware has following code : 

**It is used to authorize the jsnowebtoken stored as cookie**

const jwt=require("jsonwebtoken");
require("dotenv").config();
const Register=require("../models/registers");
const auth =async (req,res,next)=> {
    try {
        const token=req.cookies.jwt;
        const verifyUser=jwt.verify(token,process.env.SECRET_KEY);
        next();

    } catch (error) {
        res.status(400).send(error);        
    }
}
module.exports=auth;


9. register.js in src/models has following code :

**Below code declares the pattern of data, called schema**

const mongoose=require("mongoose");
const bcrypt=require("bcryptjs");
const jwt=require("jsonwebtoken");
require("dotenv").config();

const dataSchema=new mongoose.Schema({
    username:{
        type:String,
        required:true
    },
    password:{
        type:String,
        required:true
    },
    email:{
        type:String,
        required:true,
        unique:true
    },
    tokens:[{
        token:{
            type:String,
            required:true,
        }
    }]
})

**Below code generates the JWT token**

dataSchema.methods.generateToken=async function() {
    try {
        const token=jwt.sign({_id:this._id.toString()},process.env.SECRET_KEY);
        this.tokens=this.tokens.concat({token:token});
        await this.save();
        return token;

    } catch (error) {
        res.send(error);        
    }
}

**Below code is to encrypt the password entry, if there is a password in database**

dataSchema.pre("save",async function(next) {
    if(this.isModified("password")) {
    this.password=await bcrypt.hash(this.password,10);
    }
    next();
})

**Below code creates the database model and exports it**

const Register=new mongoose.model("Register",dataSchema);

module.exports=Register;



10. app.js inside src has following code : 

const express=require("express");
const path=require("path");
const app=express();
require("dotenv").config();
const port=process.env.PORT||3000;
require("./db/conn");
const hbs=require("hbs");
const Register=require("./models/registers");
const jwt=require("jsonwebtoken");
const cookieParser=require("cookie-parser");
const auth=require("./middleware/auth");
const bcrypt=require("bcryptjs");


**Below code creates paths from where the files are to be rendered**

const static_path=path.join(__dirname,"../public");
const views_path=path.join(__dirname,"../templates/views");
const partials_path=path.join(__dirname,"../templates/partials");


**Below code declares which packages will this app use**

app.use(express.json());
app.use(cookieParser());
app.use(express.urlencoded({extended:false}));
app.use(express.static(static_path));


**Below code declares the path of views and partials**

app.set("view engine","hbs");
app.set("views",views_path);
hbs.registerPartials(partials_path);


**Below code declares the different routes to be used by the app for GET method**

app.get("/",(req,res)=> {
    res.render("index");
})

app.get("/main",auth, (req,res)=> {**//JWT authorization to be used before rendering main page**
    res.render("main");
}) 

app.get("/register",(req,res)=> {
    res.render("register");
})

app.get("/login",(req,res)=> {
    res.render("login");
})


**Below code declares the different routes to be used by the app for POST method**

app.post("/register",async(req,res)=> {
    try {
        const register=new Register({
            username:req.body.username, 
            **//req.body.username means value of the input element with ID : username**
            password:req.body.password,
            email:req.body.email
        })
    const token=await register.generateToken();
    res.cookie("jwt",token,{
        expires:new Date(Date.now()+90000),// JWT expires in 90 seconds
        httpOnly:true
    });
    **Below code saves the above data taken in register object to the database** 
    const registered= await register.save();
    res.status(201).render("main");
 
    } catch (error) {
        res.status(400).send(error);
    }
})

app.post("/login",async(req,res)=> {
    try {
        const username=req.body.username;
        const password=req.body.password;
        const userName=await Register.findOne({username:username});//**search in database**
        const isMatch=await bcrypt.compare(password,userName.password);
        const token=await userName.generateToken();

        res.cookie("jwt",token,{
            expires:new Date(Date.now()+90000),
            httpOnly:true
        });


        if(isMatch) {
            res.status(201).render("main");
        }
        else {
            res.status(400).send("Invalid credentials");
               }
    } catch (error) {
        res.status(400).send(error);
    }
})


**Below code is mandatory for the webserver to listen to the port**

app.listen(port,()=> {
    console.log(`Server running at ${port}`);
}) 



11. header.hbs inside templates/partials will have the code to be included in the header of main htmls : 

<link rel="stylesheet" href="css/styles.css">


12. navbar.hbs inside templates/partials will have the code to be included inside each html's body : 

<div class="navbar">
    <a href="/main">Main</a>
    <a href="/login">Login</a>
    <a href="/register">Register</a>
    <a href="/">Home</a>
</div>



13. views folder inside templates will have all the required htmls to be rendered at different routes (/login,/register etc. used in href of anchor tags)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    {{>header}}
</head>
<body>
    {{>navbar}}
   <main class="index-main">
		<p>Kindly register above to view the main website</p>
	</main>
	
</body>
</html>

**Note the use of partials inside the views html files**



14. At last inside the .env file, write following code : 

MONGO_URI=mongodb+srv://swpnilpndey:BtF1X2jD7b4xWmaY@cluster0.qz5w9vl.mongodb.net/test;
SECRET_KEY=mynameisswapnilpandeywhoislearningjwt
// This secret key is just random string of > 32 letters

### If we want to write some JS files for these htmls like onClick of a button, we can include them in new folder called JS in the public folder and then link then in the header.hbs file inside templates/partials 

### We need to create collection mongodb cloud and link its URL in .env file accordingly. 




