<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Student Assistant</title>

<style>

body{
font-family:Arial;
margin:0;
background:linear-gradient(135deg,#0f172a,#1e293b);
color:white;
}

/* LOGIN PAGE */

#authPage{
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
height:100vh;
}

.card{
background:#1e293b;
padding:25px;
border-radius:12px;
width:260px;
text-align:center;
box-shadow:0 0 10px black;
}

.card input{
width:90%;
padding:10px;
margin:8px 0;
border:none;
border-radius:6px;
}

.card button{
width:95%;
padding:10px;
margin-top:8px;
border:none;
border-radius:6px;
background:#22c55e;
color:white;
font-weight:bold;
}

.switch{
margin-top:10px;
font-size:12px;
cursor:pointer;
color:#38bdf8;
}

/* APP */

#app{
display:none;
}

header{
background:#2563eb;
padding:15px;
text-align:center;
font-size:20px;
}

#chat{
height:60vh;
overflow:auto;
padding:10px;
background:#111827;
}

.msg{
padding:10px;
margin:8px;
border-radius:8px;
}

.user{
background:#2563eb;
}

.bot{
background:#374151;
}

#controls{
position:fixed;
bottom:0;
width:100%;
background:#020617;
padding:10px;
text-align:center;
}

#controls input{
width:60%;
padding:10px;
border:none;
border-radius:6px;
}

#controls button{
padding:10px;
margin-left:5px;
border:none;
border-radius:6px;
background:#22c55e;
color:white;
}

</style>
</head>

<body>

<!-- AUTH PAGE -->

<div id="authPage">

<div class="card">

<h2 id="title">Login</h2>

<input id="username" placeholder="Username">

<input id="password" placeholder="Password">

<button onclick="login()">Login</button>

<button onclick="signup()">Create Account</button>

<div class="switch">
Any username and password allowed
</div>

</div>

</div>

<!-- MAIN APP -->

<div id="app">

<header>🎓 AI Student Assistant</header>

<div id="chat"></div>

<div id="controls">

<input id="input" placeholder="Ask something...">

<button onclick="send()">Send</button>

</div>

</div>

<script>

/* AUTH SYSTEM */

function signup(){

let user=document.getElementById("username").value
let pass=document.getElementById("password").value

if(user==="") return alert("Enter username")

let users=JSON.parse(localStorage.getItem("users")||"{}")

users[user]=pass

localStorage.setItem("users",JSON.stringify(users))

alert("Account created")

}

function login(){

let user=document.getElementById("username").value
let pass=document.getElementById("password").value

let users=JSON.parse(localStorage.getItem("users")||"{}")

if(users[user]===pass){

document.getElementById("authPage").style.display="none"
document.getElementById("app").style.display="block"

}else{

alert("Wrong username or password")

}

}

/* CHAT */

let chat=document.getElementById("chat")

function addUser(t){
chat.innerHTML+=`<div class="msg user">You: ${t}</div>`
chat.scrollTop=chat.scrollHeight
}

function addBot(t){
chat.innerHTML+=`<div class="msg bot">Assistant: ${t}</div>`
chat.scrollTop=chat.scrollHeight
}

function speak(t){
speechSynthesis.speak(new SpeechSynthesisUtterance(t))
}

function studyTip(){

let tips=[
"Study in 25 minute sessions.",
"Revise notes daily.",
"Practice coding regularly.",
"Sleep well before exams.",
"Take small breaks while studying."
]

return tips[Math.floor(Math.random()*tips.length)]

}

function ai(command){

command=command.toLowerCase()

if(command.includes("time"))
return "Current time is "+new Date().toLocaleTimeString()

if(command.includes("date"))
return "Today is "+new Date().toDateString()

if(command.includes("open youtube")){
window.open("https://youtube.com")
return "Opening YouTube"
}

if(command.includes("open google")){
window.open("https://google.com")
return "Opening Google"
}

if(command.startsWith("search")){
let q=command.replace("search","")
window.open("https://www.google.com/search?q="+q)
return "Searching Google for "+q
}

if(command.startsWith("calc")){
try{
let exp=command.replace("calc","")
return "Result: "+eval(exp)
}catch{
return "Invalid calculation"
}
}

if(command.includes("study tip"))
return studyTip()

return "Try commands like time, date, search AI, calc 5+3, study tip"

}

function send(){

let input=document.getElementById("input")

let text=input.value

if(text==="") return

addUser(text)

let response=ai(text)

addBot(response)

speak(response)

input.value=""

}

</script>

</body>
</html>
