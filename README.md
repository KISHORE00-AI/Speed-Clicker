# Speed-Clicker
A simple reaction game where users test their speed by clicking as fast as possible. Built with HTML.
<!DOCTYPE html>
<html>
<head>
<title>Reaction Speed Challenge</title>
<style>
body{
font-family:Arial;
text-align:center;
margin-top:100px;
}
#box{
width:300px;
height:300px;
background:red;
margin:20px auto;
cursor:pointer;
}
button{
padding:10px 20px;
font-size:18px;
}
</style>
</head>

<body>

<h1>⚡ Reaction Speed Challenge</h1>
<p>Click when box turns GREEN</p>

<button onclick="startGame()">Start</button>

<div id="box"></div>

<h2 id="result"></h2>
<h3 id="best"></h3>

<script>

let startTime;
let gameActive=false;

let bestScore = localStorage.getItem("best") || null;

if(bestScore){
document.getElementById("best").innerText="Best Score: "+bestScore+" ms";
}

function startGame(){
document.getElementById("result").innerText="Wait for green...";
document.getElementById("box").style.background="red";

gameActive=false;

let delay=Math.random()*3000+2000;

setTimeout(()=>{
document.getElementById("box").style.background="green";
startTime=new Date().getTime();
gameActive=true;
},delay);
}

document.getElementById("box").onclick=function(){

if(!gameActive){
document.getElementById("result").innerText="Too early!";
return;
}

let reaction=new Date().getTime()-startTime;
document.getElementById("result").innerText="Your time: "+reaction+" ms";

if(!bestScore || reaction<bestScore){
bestScore=reaction;
localStorage.setItem("best",reaction);
document.getElementById("best").innerText="Best Score: "+reaction+" ms";
}

gameActive=false;
}

</script>

</body>
</html>
