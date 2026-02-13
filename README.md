<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FFA Chat Interface</title>
<style>
    body { margin:0; font-family:'Cavnet', cursive; background: #004d00; color: #fff; }
    #container { display:flex; flex-direction:column; height:100vh; }
    #top { display:flex; justify-content:space-between; padding:10px; background:#006400; }
    #officerBox { display:flex; flex-direction:column; }
    #commandBox { display:flex; flex-direction:column; }
    select, input { padding:5px; font-family:'Cavnet', cursive; }
    #chatArea { flex:1; overflow-y:auto; padding:10px; background:#003300; }
    .message { margin:5px 0; }
    #inputArea { display:flex; padding:10px; background:#006400; }
    #userInput { flex:1; padding:5px; font-family:'Cavnet', cursive; }
    #sendBtn { padding:5px 10px; margin-left:5px; background:#ffd700; border:none; cursor:pointer; font-family:'Cavnet', cursive; }
    .announcement { color:#ffd700; font-weight:bold; }
    .private { color:#ff69b4; }
    a { color:#ffd700; text-decoration:none; }
</style>
</head>
<body>
<div id="container">
    <div id="top">
        <div id="officerBox">
            <label>Officer Position:</label>
            <select id="officerSelect">
                <option value="Advisor">Advisor</option>
                <option value="President">President</option>
                <option value="Vice President">Vice President</option>
                <option value="Secretary">Secretary</option>
                <option value="Treasurer">Treasurer</option>
                <option value="Reporter">Reporter</option>
                <option value="Sentinel">Sentinel</option>
                <option value="Member">Member</option>
            </select>
        </div>
        <div id="commandBox">
            <label>Command Input:</label>
            <input type="text" id="commandInput" placeholder="Enter command...">
        </div>
    </div>
    <div id="chatArea"></div>
    <div id="inputArea">
        <input type="text" id="userInput" placeholder="Type a message...">
        <button id="sendBtn">Send</button>
    </div>
</div>

<script>
const chatArea = document.getElementById('chatArea');
const userInput = document.getElementById('userInput');
const sendBtn = document.getElementById('sendBtn');
const commandInput = document.getElementById('commandInput');
const officerSelect = document.getElementById('officerSelect');

let chatLocked = false;
let officerOnly = false;
let muted = false;

const ffaAnimalLinks = [
    {name: 'Tips and Tricks for Raising a Market Hog', url:'https://www.ffa.org/the-feed/tips-and-tricks-for-raising-a-market-hog/'},
    {name: 'Aggie’s Camp Inspires Youth Through Hands-On Lessons', url:'https://www.ffa.org/ffa-in-the-usa/aggies-camp-inspires-youth/'},
    {name: 'Giving Students Goat Opportunities', url:'https://www.ffa.org/ffa-in-the-usa/giving-students-goat-opportunities/'},
    {name: '6 Buzzworthy Facts About Bees and Honey', url:'https://www.ffa.org/the-feed/buzzworthy-facts-bees-honey/'},
    {name: 'Poultry SAE Hatches a Large Following', url:'https://www.ffa.org/ffa-new-horizons/poultry-sae-hatches-a-large-following/'},
    {name: 'Engineering for Elephants', url:'https://www.ffa.org/ffa-new-horizons/engineering-for-elephants/'},
    {name: 'Veterinary Science', url:'https://www.ffa.org/participate/cdes/veterinary-science/'},
    {name: 'Livestock Evaluation', url:'https://www.ffa.org/participate/cdes/livestock-evaluation/'},
    {name: 'Dairy Cattle Evaluation & Management', url:'https://www.ffa.org/participate/cdes/dairy-cattle-evaluation-management/'},
    {name: 'Horse Evaluation', url:'https://www.ffa.org/participate/cdes/horse-evaluation/'},
    {name: 'Meats Evaluation & Technology', url:'https://www.ffa.org/participate/cdes/meats-evaluation-and-technology/'}
];

const commands = {
    'clear chat': () => chatArea.innerHTML = '',
    'help': () => addMessage('Available commands: /clear chat, /help, /lock chat, /unlock chat, /mute all, /unmute all, /announce [message], /add event, /clear events, /officer only, /everyone, /animal info, /msg [user] [message]'),
    'lock chat': () => { chatLocked=true; addMessage('Chat is now locked.'); },
    'unlock chat': () => { chatLocked=false; addMessage('Chat is now unlocked.'); },
    'mute all': () => { muted=true; addMessage('All members muted.'); },
    'unmute all': () => { muted=false; addMessage('All members can speak again.'); },
    'officer only': () => { officerOnly=true; addMessage('Only officers can chat now.'); },
    'everyone': () => { officerOnly=false; addMessage('Everyone can chat now.'); },
    'add event': () => addMessage('Event creation opened (placeholder).'),
    'clear events': () => addMessage('All events cleared (placeholder).'),
    'announce': msg => addMessage(msg, 'announcement'),
    'animal info': () => {
        ffaAnimalLinks.forEach(info => {
            const a = document.createElement('a');
            a.href = info.url;
            a.target = '_blank';
            a.innerText = info.name;
            const div = document.createElement('div');
            div.className = 'message';
            div.appendChild(a);
            chatArea.appendChild(div);
        });
        chatArea.scrollTop = chatArea.scrollHeight;
    },
    'msg': parts => {
        const targetUser = parts[1];
        const message = parts.slice(2).join(' ');
        if(!targetUser || !message) return addMessage('Usage: /msg [user] [message]');
        addMessage('(Private) ' + officerSelect.value + ' to ' + targetUser + ': ' + message, 'private');
    }
};

function addMessage(msg, type='normal') {
    const div = document.createElement('div');
    div.className = 'message';
    if(type==='announcement') div.classList.add('announcement');
    if(type==='private') div.classList.add('private');
    div.innerText = msg;
    chatArea.appendChild(div);
    chatArea.scrollTop = chatArea.scrollHeight;
}

function processCommand(input) {
    if(!input.startsWith('/')) return addMessage('Commands must start with /');
    const parts = input.slice(1).split(' ');
    const cmd = parts[0].toLowerCase();
    const isAdvisor = officerSelect.value==='Advisor';

    if(cmd==='announce') {
        const msg = parts.slice(1).join(' ');
        if(isAdvisor || officerSelect.value!=='Member') commands['announce'](msg);
        else addMessage('Only officers and advisors can use this command.');
    } else if(cmd==='animal' && parts[1]==='info') {
        commands['animal info']();
    } else if(cmd==='msg') {
        commands['msg'](parts);
    } else if(commands[cmd]) {
        if(isAdvisor || officerSelect.value!=='Member') commands[cmd]();
        else addMessage('Only officers and advisors can use this command.');
    } else {
        addMessage('Unknown command. Type /help for commands.');
    }
}

sendBtn.addEventListener('click', () => {
    const msg = userInput.value.trim();
    if(!msg) return;
    if(msg.startsWith('/')) {
        processCommand(msg);
    } else {
        if(chatLocked) return addMessage('Chat is locked.');
        if(officerOnly && !['Advisor','President','Vice President','Secretary','Treasurer','Reporter','Sentinel'].includes(officerSelect.value)) return addMessage('Only officers can chat now.');
        if(muted && officerSelect.value==='Member') return addMessage('You are muted.');
        addMessage(officerSelect.value + ': ' + msg);
    }
    userInput.value='';
});

commandInput.addEventListener('keypress', e => {
    if(e.key==='Enter') {
        processCommand(commandInput.value.trim());
        commandInput.value='';
    }
});
</script>
</body>
</html>
