<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Student Assistant</title>

<style>

body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
margin:0;
}

h1{
background:#2563eb;
padding:15px;
margin:0;
}

#chat{
height:60vh;
overflow:auto;
padding:10px;
background:#1e293b;
}

.message{
margin:10px;
padding:10px;
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

input{
width:60%;
padding:10px;
border-radius:5px;
border:none;
}

button{
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

<h1>🎓 AI Student Assistant</h1>

<div id="chat"></div>

<div id="controls">

<input id="input" placeholder="Ask something..." />

<button onclick="send()">Send</button>

</div>

<script>

let chat=document.getElementById("chat")

function addUser(text){
chat.innerHTML += "<div class='message user'>You: "+text+"</div>"
chat.scrollTop=chat.scrollHeight
}

function addBot(text){
chat.innerHTML += "<div class='message bot'>Assistant: "+text+"</div>"
chat.scrollTop=chat.scrollHeight
}

function speak(text){
let speech=new SpeechSynthesisUtterance(text)
speechSynthesis.speak(speech)
}

function ai(command){

command=command.toLowerCase()

if(command.includes("time")){
return "Current time is "+new Date().toLocaleTimeString()
}

if(command.includes("date")){
return "Today is "+new Date().toDateString()
}

if(command.includes("hello")){
return "Hello student. How can I help you today?"
}

if(command.includes("open youtube")){
window.open("https://youtube.com")
return "Opening YouTube"
}

if(command.includes("open google")){
window.open("https://google.com")
return "Opening Google"
}

return "I am your AI student assistant. Ask about time, date, or websites."

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
