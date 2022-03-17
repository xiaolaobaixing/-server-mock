# -server-mock
nodejs 手写server来mock数据，

server.js部分
const http = require('http')
const fs = require('fs')
const url = require('url')
const server = http.createServer((req,res)=>{
    let urlobj = url.parse(req.url)
    console.log(urlobj)
 if(urlobj.pathname === '/getWeather') {
     res.end(JSON.stringify({data: '晴'}))
 } else{

 
  res.end(fs.readFileSync(__dirname +'/index.html'))

 }
})

server.listen(8888)

console.log('open http://localhost:8888')

index.html部分：
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
   <P>天气: <span></span></P>
   
   <script>
    let xhr = new XMLHttpRequest()
    xhr.open('GET','http://localhost:8888/getWeather',true)
    xhr.onload = function() {
       document.querySelector('span').innerText = JSON.parse(xhr.responseText).data
    }
    xhr.send()
    </script>
</body>
</html>
