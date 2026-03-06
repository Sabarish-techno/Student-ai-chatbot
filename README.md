<!DOCTYPE html>
<html>
<head>
<title>AI Smart Study Assistant</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

body{
font-family:Arial;
margin:0;
background:linear-gradient(120deg,#00c6ff,#0072ff);
text-align:center;
color:white;
}

.container{
background:white;
color:black;
width:90%;
max-width:420px;
margin:auto;
margin-top:25px;
padding:20px;
border-radius:15px;
box-shadow:0 0 10px rgba(0,0,0,0.3);
}

.robot{
font-size:70px;
}

input,textarea,select{
width:90%;
padding:10px;
margin:10px;
border-radius:8px;
border:1px solid #ccc;
}

button{
padding:10px 18px;
border:none;
border-radius:8px;
background:#0072ff;
color:white;
font-size:16px;
margin:5px;
cursor:pointer;
}

button:hover{
background:#0045aa;
}

.hidden{
display:none;
}

.chatbox{
height:200px;
overflow:auto;
border:1px solid #ccc;
padding:10px;
border-radius:8px;
text-align:left;
}

.user{color:blue;}
.bot{color:green;}

.result{
background:#f3f3f3;
padding:10px;
border-radius:8px;
margin-top:10px;
}

</style>
</head>

<body>

<h1>🤖 AI Smart Study Assistant</h1>

<!-- LOGIN -->

<div class="container" id="loginPage">

<h3>Login</h3>

<input id="username" Sabarish="username">
<input id="password" 123="password">

<button onclick="login()">Login</button>

</div>


<!-- DASHBOARD -->

<div class="container hidden" id="dashboard">

<div class="robot">🤖</div>

<h3>Welcome <span id="userDisplay"></span></h3>

<button onclick="openPage('chatPage')">AI Chat</button>
<button
