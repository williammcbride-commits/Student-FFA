<!DOCTYPE html>
<html>
<head>
<title>FFA Chapter Network</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

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
    font-weight:bold;
}

.container{
    display:flex;
    flex-wrap:wrap;
    gap:10px;
    padding:10px;
}

.box{
    background:rgba(0,0,0,0.35);
    padding:15px;
    border-radius:12px;
    flex:1;
    min-width:250px;
}

#calendar{
    display:grid;
    grid-template-columns:repeat(7,1fr);
    gap:5px;
}

.day{
    background:white;
    color:black;
    min-height:80px;
    border-radius:8px;
    padding:5px;
    cursor:pointer;
    font-size:14px;
}

.day:hover{
    background:#ffe680;
}

.event{
    font-size:12px;
    background:#0b5e2a;
    color:white;
    margin-top:3px;
    padding:2px;
    border-radius:4px;
}

.chat{
    position:fixed;
    bottom:0;
    width:100%;
    background:#0b5e2a;
    padding:10px;
}

#chatBox{
    height:150px;
    overflow:auto;
    background:white;
    color:black;
    border-radius:8px;
    padding:10px;
}

button{
    background:gold;
    border:none;
    padding:6px;
    border-radius:6px;
    cursor:pointer;
}

input,select{
    padding:6px;
    border-radius:6px;
}
</style>
</head>

<body>

<header>
FFA Chapter Network
</header>

<div class="container">

<div class="box">
<h3>Officer Position</h3>
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
<h3>Commands</h3>
<input id="commandInput">
<button onclick="runCommand()">Run</button>
<p id="commandOutput"></p>
</div>

</div>

<!-- CALENDAR -->
<div class="box" style="margin:10px;">
<h3>Chapter Calendar</h3>

<button onclick="prevMonth()">Previous</button>
<span id="monthLabel"></span>
<button onclick="nextMonth()">Next</button>

<div id="calendar"></div>

</div>

<!-- CHAT -->
<div class="chat">
<div id="chatBox"></div>
<input id="chatInput">
<button onclick="sendMessage()">Send</button>
</div>

<script>
let currentDate=new Date();

const events={};

function renderCalendar(){

    const calendar=document.getElementById("calendar");
    calendar.innerHTML="";

    let year=currentDate.getFullYear();
    let month=currentDate.getMonth();

    document.getElementById("monthLabel").innerText=
        currentDate.toLocaleString('default',{month:'long'})+" "+year;

    let firstDay=new Date(year,month,1).getDay();
    let days=new Date(year,month+1,0).getDate();

    for(let i=0;i<firstDay;i++){
        calendar.innerHTML+="<div></div>";
    }

    for(let d=1;d<=days;d++){

        let key=year+"-"+month+"-"+d;

        let div=document.createElement("div");
        div.className="day";
        div.innerHTML="<b>"+d+"</b>";

        if(events[key]){
            events[key].forEach(e=>{
                div.innerHTML+="<div class='event'>"+e+"</div>";
            });
        }

        div.onclick=function(){
            let name=prompt("Enter event");
            if(name){
                if(!events[key])events[key]=[];
                events[key].push(name);
                renderCalendar();
            }
        };

        calendar.appendChild(div);
    }
}

function prevMonth(){
currentDate.setMonth(currentDate.getMonth()-1);
renderCalendar();
}

function nextMonth(){
currentDate.setMonth(currentDate.getMonth()+1);
renderCalendar();
}

renderCalendar();


// CHAT
const banned=["badword","damn","hell"];

function filter(text){
    banned.forEach(w=>{
        let r=new RegExp(w,"gi");
        text=text.replace(r,"****");
    });
    return text;
}

function sendMessage(){

let msg=document.getElementById("chatInput").value;
let pos=document.getElementById("position").value;

if(!msg)return;

msg=filter(msg);

let box=document.getElementById("chatBox");

box.innerHTML+="<b>"+pos+":</b> "+msg+"<br>";

document.getElementById("chatInput").value="";
}


// COMMANDS
function runCommand(){

let cmd=document.getElementById("commandInput").value.toLowerCase();
let out=document.getElementById("commandOutput");

if(cmd=="clear chat"){
document.getElementById("chatBox").innerHTML="";
out.innerText="Chat cleared";
}
else if(cmd=="help"){
out.innerText="Commands: clear chat, help";
}
else{
out.innerText="Unknown command";
}

}

</script>

</body>
</html>
