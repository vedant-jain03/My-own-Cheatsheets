### Post Method Using Fetch
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

### Get Method Using Fetch
```
const _id = userid;
    const getdetail =async(e)=>{
        const userresult = await fetch('http://localhost:5000/about',{
            method:'POST',
            headers:{
                'Content-Type':'application/json'
            },
            body: JSON.stringify({
                _id
            })
        });
        if(userresult.status===200){
            const userdetail = await userresult.json();
            setdetail(userdetail.result)
            console.log(userdetail.result);
    }else{
        console.log(userresult)
    }
    }
    useEffect(()=>{
        getdetail();
    },[])
```
