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
 2. create new file config.env and put DB= '<DB Connection URL>'
 3. 
 ```
 const dotenv= require('dotenv')
 dotenv.config({path:'./config.env'})
 ```
 4. Put config.env in .gitignore file
