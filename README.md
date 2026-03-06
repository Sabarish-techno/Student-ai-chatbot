<!DOCTYPE html>
<html>
<head>
<title>AI Smart Assistant</title>

<style>

body{
font-family:Arial;
margin:0;
background:linear-gradient(45deg,#4facfe,#00f2fe);
color:white;
text-align:center;
}

h1{
margin-top:20px;
}

.container{
margin:auto;
width:90%;
max-width:400px;
background:white;
color:black;
padding:20px;
border-radius:15px;
box-shadow:0 0 10px rgba(0,0,0,0.3);
margin-top:40px;
}

input{
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
background:#4facfe;
color:white;
font-size:16px;
cursor:pointer;
}

button:hover{
background:#007bff;
}

.hidden{
display:none;
}

.robot{
font-size:80px;
}

.chatbox{
height:200px;
overflow:auto;
border:1px solid #ccc;
padding:10px;
border-radius:10px;
margin-bottom:10px;
}

.message{
margin:5px;
}

.user{
color:blue;
}

.bot{
color:green;
}

.menu button{
margin:5px;
}

</style>
</head>

<body>

<h1>🤖 AI Smart Assistant</h1>

<!-- LOGIN PAGE -->

<div class="container" id="loginPage">

<h2>Login / Create Account</h2>

<input id="username" placeholder="Username">
<input id="password" placeholder="Password">

<button onclick="login()">Login</button>

</div>


<!-- DASHBOARD -->

<div class="container hidden" id="dashboard">

<div class="robot">🤖</div>

<h2>Welcome <span id="userDisplay"></span></h2>

<div class="menu">
<button onclick="showPage('chatPage')">AI Chat</button>
<button onclick="showPage('featurePage')">Features</button>
<button onclick="logout()">Logout</button>
</div>

</div>


<!-- CHAT PAGE -->

<div class="container hidden" id="chatPage">

<h2>AI Chat</h2>

<div class="chatbox" id="chatbox"></div>

<input id="userInput" placeholder="Ask AI something...">

<button onclick="sendMessage()">Send</button>

<button onclick="back()">Back</button>

</div>


<!-- FEATURE PAGE -->

<div class="container hidden" id="featurePage">

<h2>App Features</h2>

<p>🤖 AI Chat Assistant</p>
<p>📊 Smart Suggestions</p>
<p>🌾 Crop Advice</p>
<p>📚 Study Helper</p>
<p>📅 Daily Planner</p>

<button onclick="back()">Back</button>

</div>



<script>

let currentUser="";

function login(){

let user=document.getElementById("username").value;
let pass=document.getElementById("password").value;

if(user.length>0 && pass.length>0){

currentUser=user;

document.getElementById("loginPage").classList.add("hidden");
document.getElementById("dashboard").classList.remove("hidden");

document.getElementById("userDisplay").innerText=user;

}

else{

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
document.getElementById("featurePage").classList.add("hidden");

document.getElementById("dashboard").classList.remove("hidden");

}

function sendMessage(){

let input=document.getElementById("userInput");
let text=input.value;

if(text==="") return;

let chat=document.getElementById("chatbox");

chat.innerHTML+=`<div class="message user">You: ${text}</div>`;

let reply=getAIResponse(text);

chat.innerHTML+=`<div class="message bot">AI: ${reply}</div>`;

input.value="";

chat.scrollTop=chat.scrollHeight;

}

function getAIResponse(msg){

msg=msg.toLowerCase();

if(msg.includes("hello")) return "Hello! I am your AI assistant 🤖";

if(msg.includes("ai")) return "AI means machines that can learn and think.";

if(msg.includes("study")) return "Study 1 hour daily and practice coding.";

if(msg.includes("project")) return "You can build AI apps using Python or Java.";

if(msg.includes("crop")) return "Check crop leaves and use disease detection AI.";

return "Interesting question! I am still learning.";

}

</script>

</body>
</html>
