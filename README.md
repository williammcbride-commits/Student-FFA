<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FFA Chapter Network</title>
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-database-compat.js"></script>
<style>
  body { font-family: 'Caveat', cursive; background: linear-gradient(135deg, #006400, #FFD700); margin:0; height:100vh; display:flex; flex-direction:column;}
  #top { display:flex; justify-content: space-between; padding:10px; background:rgba(255,255,255,0.2);}
  #officerSelect { width:200px; }
  #commandInput { width:300px; }
  #chat { flex:1; padding:10px; overflow-y:auto; border-top:2px solid #fff; background:rgba(255,255,255,0.1);}
  #messageInput { width:calc(100% - 20px); padding:5px; margin:5px; }
  .message { margin-bottom:10px; }
  .admin { font-weight:bold; color:red; }
  .animal-info { background:rgba(255,255,255,0.3); margin:5px; padding:5px; border-radius:5px; }
  button { cursor:pointer; padding:3px 6px; margin-left:5px; }
</style>
</head>
<body>
  <div id="top">
    <select id="officerSelect">
      <option value="">Select Officer Position</option>
      <option value="President">President</option>
      <option value="Vice President">Vice President</option>
      <option value="Secretary">Secretary</option>
      <option value="Treasurer">Treasurer</option>
      <option value="Reporter">Reporter</option>
      <option value="Sentinel">Sentinel</option>
    </select>
    <input type="text" id="commandInput" placeholder="Enter command here...">
  </div>

  <div id="chat"></div>
  <input type="text" id="messageInput" placeholder="Type message...">

<script>
  // Firebase configuration
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT.firebaseio.com",
    projectId: "YOUR_PROJECT",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "SENDER_ID",
    appId: "APP_ID"
  };
  firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();
  const db = firebase.database();

  // Sign in anonymously for demo
  auth.signInAnonymously();

  const chatDiv = document.getElementById('chat');
  const msgInput = document.getElementById('messageInput');
  const cmdInput = document.getElementById('commandInput');
  const officerSelect = document.getElementById('officerSelect');

  let officerPosition = "";
  officerSelect.addEventListener('change', () => {
    officerPosition = officerSelect.value;
  });

  function addMessage(user, text, isAdmin=false) {
    const div = document.createElement('div');
    div.className = 'message' + (isAdmin ? ' admin' : '');
    div.innerHTML = `<b>${user}:</b> ${text}`;
    chatDiv.appendChild(div);
    chatDiv.scrollTop = chatDiv.scrollHeight;
  }

  // Load messages
  db.ref('messages').on('child_added', snapshot => {
    const msg = snapshot.val();
    addMessage(msg.user, msg.text, msg.isAdmin);
  });

  // Send message
  msgInput.addEventListener('keypress', e => {
    if(e.key==='Enter'){
      const text = msgInput.value.trim();
      if(!text) return;
      db.ref('messages').push({ user: officerPosition || 'Member', text, isAdmin:false });
      msgInput.value='';
    }
  });

  // Commands system
  cmdInput.addEventListener('keypress', e => {
    if(e.key==='Enter'){
      const cmd = cmdInput.value.trim().toLowerCase();
      cmdInput.value='';
      if(cmd === '/animalinfo'){
        // All animal info from your previous pages
        const animals = [
          { name: "Goats", link:"https://www.ffa.org/ffa-in-the-usa/giving-students-goat-opportunities/" },
          { name: "Bees", link:"https://www.ffa.org/the-feed/buzzworthy-facts-bees-honey/" },
          { name: "Dogs", link:"https://www.ffa.org/ffa-in-the-usa/raise-a-life-change-a-life/" },
          { name: "Cattle", link:"https://www.ffa.org/the-feed/cambridge-ffa-develops-spanish-learning-program/" },
          { name: "Horses", link:"https://www.ffa.org/participate/cdes/horse-evaluation/" },
          { name: "Poultry", link:"https://www.ffa.org/participate/poultry/" },
          { name: "Dairy Cattle", link:"https://www.ffa.org/participate/cdes/dairy-cattle-evaluation-management/" },
          { name: "Elephants", link:"https://www.ffa.org/ffa-new-horizons/engineering-for-elephants/" }
        ];
        animals.forEach(a => addMessage("Animal Info", `<a href="${a.link}" target="_blank">${a.name}</a>`));
      }
      else if(cmd === '/help'){
        addMessage("System", "Available commands: /animalinfo, /help, /clear, /ai");
      }
      else if(cmd === '/clear'){
        chatDiv.innerHTML='';
      }
      else if(cmd.startsWith('/ai')){
        const userQuery = cmd.slice(4);
        addMessage("FFA AI", `You asked: ${userQuery} <br>Response: Sorry! AI module placeholder.`);
      }
      else{
        addMessage("System", "Unknown command. Type /help");
      }
    }
  });

  // Admin Panel: delete messages
  chatDiv.addEventListener('click', e => {
    if(e.target.classList.contains('message') && confirm("Delete this message?")){
      e.target.remove();
    }
  });
</script>
</body>
</html>
