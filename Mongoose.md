### Connection
``` const mongoose = require('mongoose') ```

### Connection with MongoDB CLuster
```
 1. create cluster
 2. database
 3. network
```
### connection with backend
```
const DB = 'connection URL';
mongoose.connect(DB,{
    useNewUrlParser: true,
    useFindAndModify:false,
    useUnifiedTopology: true,
    useCreateIndex: true
}).then(()=>{
    try{
       console.log('Connected');
    }catch(err){
       console.log(err);
    }
})
```
### Secure Mongo using dotenv
 1. ```npm i dotenv```
 2. create new file config.env and put DB= 'DB Connection URL'
 3. 
 ```
 const dotenv= require('dotenv')
 dotenv.config({path:'./config.env'})
 ```
 4. Put config.env in .gitignore file

### Schema and Model
```Schema defines the structure of our Document.```
``` 
// Creating New Schema
const MySchema = new mongoose.Schema({
   name:{
      type: String,
      require: true
   },
   Phone:{
      type: Number,
      require: true
   }
})
```
```
// Creating a Model
const ModelName = mongoose.model('collection name(singular)',schemaname);
```

### Routing
```
const express=require('express')
const router = express.Router();
router.get('/',(req,res)=>{
    res.status(200).json(req.body);
})
```

### User Registration
```
const User = require('Schema Model Path');
router.get('/register',async (req,res)=>{
    // Destructure Schema 
    const {name,email,phone,work,password,cpassword}= req.body;
    
    if(!name || !email || ....){
        res.status(509).json({message:"Empty Field"})
    }else if(password !== cpassword){
        res.status(509).json({message:"Password not matches"})
    }
    try{
       const userexist = await User.findOne({email:email})
       if(userexist){
          return res.status(500).json({message:"User Already Exist"});
       }
       const user = new User({name,email,phone,work,password,cpassword});
       const userregister = await user.save();
       if(userregister){
          res.status(200).json({message:"User Registered"});
       }else{
          res.status(500).json({message:"Registration Failed"});
       }
    }catch((err)=>{
       console.log(err);
       res.status(500).json({message:"Error "})
    })
})
```

### User Login
```
// Login Registration
router.post('/signin',async (req,res)=>{
    const {email,password}=req.body;
    if(!email || !password){
        return res.status(509).json({message:'Empty Fields'});
    }
    try{
        const useremail= await User.findOne({email:email})
        const userpassword= await bcrypt.compare(password, useremail.password);
        if(useremail && !userpassword){
            return res.status(500).json({message:'Password is Wrong'})
        }
        else if(!useremail || !userpassword){
            return res.status(500).json({message:'User Not Found '})
        }
        res.status(200).json({message:'Login Succesful'});
    }catch(err){
        console.log(err);
    }
})
```

### Password Security using Hashing
1. ```npm i bcryptjs```
2. ```const bcrypt = require('bcryptjs')```
3. In user schema model before exporting module
 ```
 // This will act as a Middleware between requestion and mongoose.save() method
 userschema.pre('save',async (next)=>{
    console.log('Hashed Successfully');
    if(this.isModified('password')){
        this.password = await bcrypt.hash('password',12);
        this.cpassword = await bcrypt.hash('cpassword',12);
    }
    next();
 })
 ```
