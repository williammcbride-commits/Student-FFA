<!DOCTYPE html>
<html>
<head>
<title>FFA Chapter Network Complete</title>

<style>
body{
margin:0;
font-family:Arial;
background:linear-gradient(to bottom right,#0b5e2a,#d4af37);
color:white;
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

#calendar{
display:grid;
grid-template-columns:repeat(7,1fr);
gap:5px;
padding:10px;
}

.day{
background:white;
color:black;
min-height:80px;
border-radius:6px;
padding:5px;
cursor:pointer;
}

.event{
background:#0b5e2a;
color:white;
margin-top:3px;
border-radius:4px;
padding:2px;
font-size:12px;
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
margin:3px;
}
</style>
</head>

<body>

<header>FFA Chapter Network</header>

<div class="top">

<div class="box">
Officer Position<br>
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
Command Box<br>
<input id="commandInput">
<button onclick="runCommand()">Run</button>
<div id="output"></div>
</div>

</div>

<div class="box">

<button onclick="prevMonth()">Prev</button>
<span id="month"></span>
<button onclick="nextMonth()">Next</button>

<div id="calendar"></div>

</div>

<div id="chatBox"></div>

<div class="chatInput">
<input id="chatInput">
<button onclick="sendMessage()">Send</button>
</div>

<script>

let chatLocked=false;
let officerOnly=false;
let muted=false;

const officers=[
"President",
"Vice President",
"Secretary",
"Treasurer",
"Reporter",
"Sentinel"
];

const banned=["badword","hell","damn"];

function filter(msg){
banned.forEach(w=>{
msg=msg.replace(new RegExp(w,"gi"),"****");
});
return msg;
}

function isOfficer(){
let pos=document.getElementById("position").value;
return officers.includes(pos);
}

function sendMessage(){

if(chatLocked)return;

if(officerOnly && !isOfficer())return;

if(muted && !isOfficer())return;

let msg=document.getElementById("chatInput").value;

msg=filter(msg);

let pos=document.getElementById("position").value;

chatBox.innerHTML+=pos+": "+msg+"<br>";

}

function runCommand(){

let cmd=document.getElementById("commandInput").value.toLowerCase();

let out=document.getElementById("output");

if(cmd=="help"){

out.innerHTML=`
clear chat<br>
lock chat<br>
unlock chat<br>
mute all<br>
unmute all<br>
announce [message]<br>
add event<br>
clear events<br>
officer only<br>
everyone<br>
animal careers<br>
animal systems<br>
vet info<br>
ffa awards<br>
ffa news<br>
`;

}

else if(cmd=="clear chat"){
chatBox.innerHTML="";
}

else if(cmd=="lock chat"){
chatLocked=true;
}

else if(cmd=="unlock chat"){
chatLocked=false;
}

else if(cmd=="mute all"){
muted=true;
}

else if(cmd=="unmute all"){
muted=false;
}

else if(cmd=="officer only"){
officerOnly=true;
}

else if(cmd=="everyone"){
officerOnly=false;
}

else if(cmd.startsWith("announce")){

let msg=cmd.replace("announce","");

chatBox.innerHTML+=
"<div class='announcement'>ANNOUNCEMENT:"+msg+"</div>";

}

else if(cmd=="clear events"){
events={};
renderCalendar();
}

else if(cmd=="animal careers"){
alert("FFA members explore careers like veterinary science, livestock production, animal nutrition, and animal biotechnology.");
}

else if(cmd=="animal systems"){
alert("Animal systems include breeding, feeding, animal health, genetics, and livestock management.");
}

else if(cmd=="vet info"){
alert("Veterinary careers include veterinarians, vet technicians, and animal scientists.");
}

else if(cmd=="ffa awards"){
alert("FFA offers Agriscience Fair awards, proficiency awards, and American Star awards.");
}

else if(cmd=="ffa news"){
alert("FFA members attend conventions, leadership conferences, and career exploration events.");
}

else{
out.innerText="Unknown command";
}

}


// CALENDAR

let date=new Date();
let events={};

function renderCalendar(){

calendar.innerHTML="";

let year=date.getFullYear();
let month=date.getMonth();

monthLabel.innerText=
date.toLocaleString("default",{month:"long"})+" "+year;

let first=new Date(year,month,1).getDay();
let days=new Date(year,month+1,0).getDate();

for(let i=0;i<first;i++){
calendar.innerHTML+="<div></div>";
}

for(let d=1;d<=days;d++){

let key=year+"-"+month+"-"+d;

let div=document.createElement("div");

div.className="day";

div.innerHTML=d;

if(events[key]){
events[key].forEach(e=>{
div.innerHTML+="<div class='event'>"+e+"</div>";
});
}

div.onclick=function(){

let name=prompt("Event name");

if(!events[key])events[key]=[];

events[key].push(name);

renderCalendar();

};

calendar.appendChild(div);

}

}

function prevMonth(){
date.setMonth(date.getMonth()-1);
renderCalendar();
}

function nextMonth(){
date.setMonth(date.getMonth()+1);
renderCalendar();
}

renderCalendar();

</script>

</body>
</html>
