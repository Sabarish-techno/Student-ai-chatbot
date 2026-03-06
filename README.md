<!DOCTYPE html>
<html>
<head>
<title>AI Smart Study Assistant</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

body{
font-family:Arial;
margin:0;
background:linear-gradient(45deg,#00c6ff,#0072ff);
color:white;
text-align:center;
}

.container{
margin:auto;
width:90%;
max-width:420px;
background:white;
color:black;
padding:20px;
border-radius:15px;
box-shadow:0 0 10px rgba(0,0,0,0.3);
margin-top:25px;
}

.robot{
font-size:70px;
}

input,textarea,select{
width:90%;
padding:10px;
margin:10px;
border-radius:10px;
border:1px solid #ccc;
}

button{
padding:10px 20px;
border:none;
border-radius:10px;
background:#0072ff;
color:white;
font-size:16px;
cursor:pointer;
margin:5px;
}

button:hover{
background:#0047ab;
}

.hidden{
display:none;
}

.chatbox{
height:200px;
overflow:auto;
border:1px solid #ccc;
padding:10px;
border-radius:10px;
margin-bottom:10px;
text-align:left;
}

.user{color:blue;}
.bot{color:green;}

.result{
background:#f2f2f2;
padding:10px;
border-radius:10px;
margin-top:10px;
}

</style>
</head>

<body>

<h1>🤖 AI Smart Study Assistant</h1>

<!-- LOGIN -->

<div class="container" id="loginPage">

<h2>Login</h2>

<input id="username" placeholder="Username">

<input id="password" placeholder="Password">

<button onclick="login()">Login</button>

</div>

<!-- DASHBOARD -->

<div class="container hidden" id="dashboard">

<div class="robot">🤖</div>

<h3>Welcome <span id="userDisplay"></span></h3>

<button onclick="showPage('chatPage')">AI Chat</button>

<button onclick="showPage('topicPage')">Topic Analyzer</button>

<button onclick="showPage('rPage')">R Programming</button>

<button onclick="showPage('osPage')">Operating System</button>

<button onclick="logout()">Logout</button>

</div>

<!-- CHAT -->

<div class="container hidden" id="chatPage">

<h3>AI Chat</h3>

<div class="chatbox" id="chatbox"></div>

<input id="userInput" placeholder="Ask something">

<button onclick="sendMessage()">Send</button>

<button onclick="startVoice()">🎤 Speak</button>

<button onclick="back()">Back</button>

</div>

<!-- TOPIC ANALYZER -->

<div class="container hidden" id="topicPage">

<h3>📚 Topic Analyzer</h3>

<textarea id="notes" rows="6" placeholder="Paste study notes"></textarea>

<button onclick="analyzeTopics()">Analyze</button>

<div id="topicResult" class="result"></div>

<button onclick="back()">Back</button>

</div>

<!-- R PROGRAMMING -->

<div class="container hidden" id="rPage">

<h3>📊 R Programming Helper</h3>

<select id="rTopic">

<option>Introduction</option>
<option>Data Types</option>
<option>Vectors</option>
<option>Functions</option>
<option>Data Frames</option>

</select>

<button onclick="showR()">Explain</button>

<div id="rResult" class="result"></div>

<button onclick="back()">Back</button>

</div>

<!-- OPERATING SYSTEM -->

<div class="container hidden" id="osPage">

<h3>💻 Operating System Helper</h3>

<select id="osTopic">

<option>Process</option>
<option>Scheduling</option>
<option>Virtual Memory</option>
<option>Deadlock</option>
<option>File System</option>

</select>

<button onclick="showOS()">Explain</button>

<div id="osResult" class="result"></div>

<button onclick="back()">Back</button>

</div>

<script>

function login(){

let user=document.getElementById("username").value;
let pass=document.getElementById("password").value;

if(user.length>0 && pass.length>0){

document.getElementById("loginPage").classList.add("hidden");

document.getElementById("dashboard").classList.remove("hidden");

document.getElementById("userDisplay").innerText=user;

}else{

alert("Enter username and password");

}

}

function logout(){
location.reload();
}

function showPage(page){

document.getElementById("dashboard").classList.add("hidden");

document.getElementById(page).classList.remove("hidden");

}

function back(){

document.getElementById("chatPage").classList.add("hidden");

document.getElementById("topicPage").classList.add("hidden");

document.getElementById("rPage").classList.add("hidden");

document.getElementById("osPage").classList.add("hidden");

document.getElementById("dashboard").classList.remove("hidden");

}

function sendMessage(){

let input=document.getElementById("userInput");

let text=input.value;

if(text==="") return;

let chat=document.getElementById("chatbox");

chat.innerHTML+=`<div class="user">You: ${text}</div>`;

let reply=getAIResponse(text);

chat.innerHTML+=`<div class="bot">AI: ${reply}</div>`;

input.value="";

chat.scrollTop=chat.scrollHeight;

}

function getAIResponse(msg){

msg=msg.toLowerCase();

if(msg.includes("hello")) return "Hello! I am your AI assistant 🤖";

if(msg.includes("ai")) return "Artificial Intelligence allows machines to learn from data.";

if(msg.includes("study")) return "Use the Topic Analyzer to find important exam topics.";

if(msg.includes("project")) return "You can build AI apps like chatbots, prediction systems, and analyzers.";

return "Interesting question! I am still learning.";

}

function startVoice(){

const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

if(!SpeechRecognition){
alert("Voice recognition not supported");
return;
}

const recognition=new SpeechRecognition();

recognition.lang="en-US";

recognition.start();

recognition.onresult=function(event){

let speech=event.results[0][0].transcript;

document.getElementById("userInput").value=speech;

sendMessage();

};

}

function analyzeTopics(){

let text=document.getElementById("notes").value.toLowerCase();

let words=text.split(/\W+/);

let stop=["the","is","a","an","and","of","to","in","on","for"];

let freq={};

words.forEach(w=>{
if(!stop.includes(w) && w.length>3){
freq[w]=(freq[w]||0)+1;
}
});

let sorted=Object.entries(freq).sort((a,b)=>b[1]-a[1]).slice(0,8);

let result="<b>Important Topics:</b><br>";

sorted.forEach(t=>{
result+=t[0]+"<br>";
});

document.getElementById("topicResult").innerHTML=result;

}

function showR(){

let topic=document.getElementById("rTopic").value;

let data={

"Introduction":"R is a programming language used for statistical computing and data analysis.",

"Data Types":"R data types include numeric, character, logical, and complex.",

"Vectors":"Vectors store multiple elements of the same type.",

"Functions":"Functions are reusable code blocks created using function().",

"Data Frames":"Data frames store tabular data in rows and columns."

};

document.getElementById("rResult").innerText=data[topic];

}

function showOS(){

let topic=document.getElementById("osTopic").value;

let data={

"Process":"A process is a program that is currently running.",

"Scheduling":"Scheduling determines which process gets CPU time.",

"Virtual Memory":"Virtual memory allows systems to use disk space as RAM.",

"Deadlock":"Deadlock occurs when processes wait for resources indefinitely.",

"File System":"File system manages files stored on disks."

};

document.getElementById("osResult").innerText=data[topic];

}

</script>

</body>
</html>
