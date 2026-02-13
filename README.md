<!DOCTYPE html>
<html>
<head>
<title>FFA Chapter Network Online</title>

<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js"></script>

<style>

body{
font-family:Arial;
background:linear-gradient(to bottom right,#0b5e2a,#d4af37);
color:white;
margin:0;
}

header{
text-align:center;
padding:15px;
font-size:28px;
}

.top{
display:flex;
justify-content:space-between;
padding:10px;
}

.box{
background:rgba(0,0,0,0.4);
padding:10px;
border-radius:10px;
}

#chatBox{
position:fixed;
bottom:60px;
width:100%;
height:200px;
background:white;
color:black;
overflow:auto;
}

.chatInput{
position:fixed;
bottom:0;
width:100%;
background:#0b5e2a;
padding:10px;
}

.announcement{
background:gold;
color:black;
padding:5px;
}

</style>

</head>

<body>

<header>FFA Chapter Network Online</header>

<div class="top">

<div class="box">

Officer Position

<select id="position">

<option>President</option>
<option>Vice President</option>
<option>Secretary</option>
<option>Treasurer</option>
<option>Reporter</option>
<option>Sentinel</option>
<option>Member</option>

</select>

</div>

<div class="box">

Command

<input id="commandInput">

<button onclick="runCommand()">Run</button>

</div>

</div>

<div id="chatBox"></div>

<div class="chatInput">

<input id="chatInput">

<button onclick="sendMessage()">Send</button>

</div>

<script>

// PASTE YOUR FIREBASE CONFIG HERE

const firebaseConfig = {

apiKey: "PASTE",
authDomain: "PASTE",
databaseURL: "PASTE",
projectId: "PASTE",
storageBucket: "PASTE",
messagingSenderId: "PASTE",
appId: "PASTE"

};

firebase.initializeApp(firebaseConfig);

const db = firebase.database();

const officers = [
"President",
"Vice President",
"Secretary",
"Treasurer",
"Reporter",
"Sentinel"
];

const banned = ["badword","hell","damn"];

function filter(msg){

banned.forEach(word=>{

msg=msg.replace(new RegExp(word,"gi"),"****");

});

return msg;

}

function sendMessage(){

let pos=document.getElementById("position").value;

let msg=document.getElementById("chatInput").value;

msg=filter(msg);

db.ref("chat").push({

position:pos,
message:msg,
time:Date.now()

});

}

db.ref("chat").on("child_added", snapshot=>{

let data=snapshot.val();

let div=document.createElement("div");

div.innerText=data.position+": "+data.message;

chatBox.appendChild(div);

chatBox.scrollTop=chatBox.scrollHeight;

});

function runCommand(){

let cmd=document.getElementById("commandInput").value;

if(cmd.startsWith("announce")){

let msg=cmd.replace("announce","");

db.ref("announcements").push({

message:msg

});

}

if(cmd=="clear chat"){

db.ref("chat").remove();

chatBox.innerHTML="";

}

}

db.ref("announcements").on("child_added", snapshot=>{

let data=snapshot.val();

let div=document.createElement("div");

div.className="announcement";

div.innerText="ANNOUNCEMENT: "+data.message;

chatBox.appendChild(div);

});

</script>

</body>
</html>
