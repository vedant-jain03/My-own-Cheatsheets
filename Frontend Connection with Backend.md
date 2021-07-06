### Using Fetch
```
const handlesubmit=async(e)=>{
e.preventDefault();
const res = await fetch("http://localhost:5000/register",{
   method: 'POST',
   headers: {
      "Content-Type":"application/json"
   },
   body: JSON.stringify({
       //your states
       name,email,.....
   })
})
if(res.status===200){
   history.push('/Homepage')
}
else{
   console.log(err);
}
}
```
