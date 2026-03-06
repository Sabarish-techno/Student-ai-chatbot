<!DOCTYPE html>
<html>
<head>
<title>AI Student Assistant</title>

<style>
body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
}

#chat{
width:80%;
height:300px;
margin:auto;
border:1px solid gray;
overflow:auto;
padding:10px;
background:#1e293b;
}

input{
width:60%;
padding:10px;
margin-top:10px;
}

button{
padding:10px 15px;
margin:5px;
background:#38bdf8;
border:none;
cursor:pointer;
}

h1{
color:#38bdf8;
}
</style>
</head>

<body>

<h1>🎓 AI Student Assistant</h1>

<div id="chat"></div>

<input id="input" placeholder="Ask something..." />
<br>

<button onclick="send()">Send</button>
<button onclick="voice()">🎤 Speak</button>

<script>

const chat=document.getElementById("chat")

function add(text){
chat.innerHTML+=text+"<br>"
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
return "Today's date is "+new Date().toDateString()
}

if(command.includes("open youtube")){
window.open("https://youtube.com")
return "Opening YouTube"
}

if(command.includes("open google")){
window.open("https://google.com")
return "Opening Google"
}

if(command.includes("hello")){
return "Hello student. How can I help you?"
}

return "I am your AI student assistant. Ask about time, date, or open websites."
}

function send(){

let input=document.getElementById("input")
let text=input.value

add("<b>You:</b> "+text)

let response=ai(text)

add("<b>Assistant:</b> "+response)

speak(response)

input.value=""
}

function voice(){

let recognition=new webkitSpeechRecognition()

recognition.onresult=function(event){

let text=event.results[0][0].transcript

add("<b>You:</b> "+text)

let response=ai(text)

add("<b>Assistant:</b> "+response)

speak(response)

}

recognition.start()

}

</script>

</body>
</html>
