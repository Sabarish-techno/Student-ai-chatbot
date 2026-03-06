<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Student Assistant</title>

<style>

body{
font-family:Arial;
margin:0;
background:#0f172a;
color:white;
}

header{
background:#2563eb;
padding:15px;
text-align:center;
font-size:20px;
}

#loginPage{
display:flex;
flex-direction:column;
align-items:center;
justify-content:center;
height:100vh;
}

#loginPage input{
padding:10px;
margin:5px;
width:200px;
border:none;
border-radius:5px;
}

#loginPage button{
padding:10px;
border:none;
background:#22c55e;
color:white;
border-radius:5px;
}

#app{
display:none;
}

#chat{
height:60vh;
overflow:auto;
padding:10px;
background:#1e293b;
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
background:#334155;
}

#controls{
position:fixed;
bottom:0;
width:100%;
background:#111827;
padding:10px;
}

#controls input{
width:60%;
padding:10px;
border:none;
border-radius:5px;
}

#controls button{
padding:10px;
border:none;
border-radius:5px;
background:#22c55e;
color:white;
margin-left:5px;
}

</style>
</head>

<body>

<!-- LOGIN PAGE -->

<div id="loginPage">

<h2>Student Login</h2>

<input id="username" placeholder="Username">

<input id="password" type="password" placeholder="Password">

<button onclick="login()">Login</button>

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

function login(){

let user=document.getElementById("username").value
let pass=document.getElementById("password").value

if(user==="student" && pass==="1234"){

document.getElementById("loginPage").style.display="none"
document.getElementById("app").style.display="block"

}else{

alert("Invalid login")

}

}

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
"Practice coding every day.",
"Sleep well before exams.",
"Teach others to remember better."
]

return tips[Math.floor(Math.random()*tips.length)]

}

function saveNote(text){

let notes=localStorage.getItem("notes")||""
notes+=text+" | "
localStorage.setItem("notes",notes)

return "Note saved"

}

function showNotes(){

let notes=localStorage.getItem("notes")

if(!notes) return "No notes saved"

return notes

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

if(command.startsWith("note")){
let n=command.replace("note","")
return saveNote(n)
}

if(command.includes("show notes"))
return showNotes()

if(command.includes("study tip"))
return studyTip()

return "Try commands: time, date, search AI, calc 5+3, note text, study tip"

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
