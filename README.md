<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FFA Chapter Network Platform</title>

<style>
:root {
  --ffa-blue: #0033A0;
  --ffa-gold: #FFB81C;
  --light-bg: #f4f6fb;
}
body {
  margin:0; font-family:'Arial', sans-serif; background:var(--light-bg); color:#222;
}
header { background:var(--ffa-blue); color:white; padding:1rem; text-align:center; }
nav { background:var(--ffa-gold); padding:0.5rem; text-align:center; }
nav a { margin:0 10px; text-decoration:none; color:#000; font-weight:bold; }
section { padding:2rem; max-width:1100px; margin:auto; }
.card { background:white; padding:1rem; margin:1rem 0; border-radius:8px; box-shadow:0 2px 6px rgba(0,0,0,0.1);}
.animals img { width:100%; max-width:300px; border-radius:10px; margin:10px; }
.topic-btn { background:var(--ffa-gold); color:#000; border:none; padding:8px 12px; margin:5px; border-radius:5px; cursor:pointer; font-weight:bold; }
.topic-btn:hover { opacity:0.8; }
footer { text-align:center; padding:1rem; background:var(--ffa-blue); color:white; margin-top:2rem; }
#chatBox, #msgBox { border:1px solid #ccc; padding:10px; height:250px; overflow-y:auto; margin-bottom:10px; background:#fff; }
input { padding:8px; width:70%; }
button { background:var(--ffa-blue); color:white; border:none; padding:10px 15px; border-radius:6px; cursor:pointer; margin-top:5px; }
button:hover { opacity:0.9; }
.user-msg { text-align:right; color:var(--ffa-blue); margin:5px 0; }
.ai-msg { text-align:left; color:var(--ffa-gold); margin:5px 0; }
html { scroll-behavior:smooth; }
@media(max-width:600px){ input {width:100%; margin-bottom:10px;} button,.topic-btn{width:100%;} }
</style>
</head>
<body>

<header>
  <h1>FFA Chapter Network Platform</h1>
  <p>Leadership • Agriculture • Education</p>
</header>

<nav>
  <a href="#animals">Animals</a>
  <a href="#creed">FFA Creed</a>
  <a href="#ai">FFA AI Help</a>
  <a href="#messaging">Chapter Messenger</a>
  <a href="#ffaOrg">Official FFA.org</a>
</nav>

<!-- Animals Section -->
<section id="animals">
  <h2>Common FFA Livestock & Animals</h2>
  <div class="card animals">
    <h3>Cattle</h3>
    <img src="https://upload.wikimedia.org/wikipedia/commons/4/4c/Cow_female_black_white.jpg" alt="Cow">
    <p>Used in beef and dairy production. Featured in livestock judging competitions.</p>
    <h3>Pigs</h3>
    <img src="https://upload.wikimedia.org/wikipedia/commons/5/5c/Pig_in_a_field.jpg" alt="Pig">
    <p>Raised for meat. Important in swine production and competitions.</p>
    <h3>Chickens</h3>
    <img src="https://upload.wikimedia.org/wikipedia/commons/7/70/Chicken_sitting.jpg" alt="Chicken">
    <p>Raised for eggs and meat. Featured in poultry judging CDEs.</p>
    <h3>Sheep</h3>
    <img src="https://upload.wikimedia.org/wikipedia/commons/8/8c/Sheep_on_grass.jpg" alt="Sheep">
    <p>Raised for wool and meat. Common in livestock judging events.</p>
  </div>
</section>

<!-- FFA Creed -->
<section id="creed">
  <h2>FFA Creed</h2>
  <div class="card">
    <p>
      <strong>The FFA Creed:</strong><br>
      I believe in the future of agriculture, with a faith born not of words but of deeds — achievements won by the present and past generations of agriculturists; in the promise of better days through better ways, even as the better things we now enjoy have come to us from the struggles of former years.<br>
      I believe that to live and work on a good farm, or to be engaged in other agricultural pursuits, is pleasant as well as challenging; for I know the joys and discomforts of agricultural life and hold an inborn fondness for those associations which, even in hours of discouragement, I cannot deny.<br>
      I believe in leadership from ourselves and respect from others. I believe in my own ability to work efficiently and think clearly, with such knowledge and skill as I can secure, and in the ability of progressive agriculturists to serve our own and the public interest in producing and marketing the product of our toil.<br>
      I believe in less dependence on begging and more power in bargaining; in the life abundant and enough honest wealth to help make it so — for others as well as myself; in less need for charity and more of it when needed; in being happy myself and playing square with those whose happiness depends upon me.<br>
      I believe that American agriculture can and will hold true to the best traditions of our national life and that I can exert an influence in my home and community which will stand solid for my part in that inspiring task.
    </p>
  </div>
</section>

<!-- FFA AI Study Assistant -->
<section id="ai">
  <h2>FFA AI Study Assistant</h2>
  <div class="card">
    <div>
      <strong>Quick Topics:</strong><br>
      <button class="topic-btn" onclick="fillTopic('FFA Creed')">FFA Creed</button>
      <button class="topic-btn" onclick="fillTopic('CDE')">CDEs</button>
      <button class="topic-btn" onclick="fillTopic('SAE')">SAEs</button>
      <button class="topic-btn" onclick="fillTopic('Officers')">Officers</button>
      <button class="topic-btn" onclick="fillTopic('Animals')">Animals</button>
      <button class="topic-btn" onclick="fillTopic('Leadership')">Leadership</button>
      <button class="topic-btn" onclick="fillTopic('Chapter')">Chapter Info</button>
    </div>
    <br>
    <div id="chatBox"></div>
    <input type="text" id="userInput" placeholder="Ask any FFA question...">
    <button onclick="askAI()">Ask</button>
    <button onclick="document.getElementById('chatBox').innerHTML = ''">Clear Chat</button>
  </div>
</section>

<!-- Chapter Messenger -->
<section id="messaging">
  <h2>FFA Chapter Messenger</h2>
  <div class="card">
    <div id="loginDiv">
      <p>Enter a username to join the chat:</p>
      <input type="text" id="usernameInput" placeholder="Your Name">
      <button onclick="loginUser()">Login</button>
      <p id="loginStatus" style="color:red;"></p>
    </div>

    <div id="messengerDiv" style="display:none;">
      <div id="msgBox"></div>
      <input type="text" id="msgInput" placeholder="Type a message...">
      <button onclick="sendMessage()">Send</button>
      <button onclick="clearMessages()">Clear Messages</button>
    </div>
  </div>
</section>

<!-- FFA.org Embed -->
<section id="ffaOrg">
  <h2>Official FFA.org Website</h2>
  <div class="card">
    <p>Access the official FFA website for up-to-date news and resources:</p>
    <a href="https://www.ffa.org/" target="_blank">Go to FFA.org</a>
  </div>
</section>

<footer>
  © 2026 FFA Chapter Network | Built for Education
</footer>

<script>
  // ===================== FFA AI using ChatGPT API =====================
  async function askChatGPT(question) {
    const response = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer YOUR_OPENAI_API_KEY" // Replace with your OpenAI key
      },
      body: JSON.stringify({
        model: "gpt-4",
        messages: [{role: "user", content: `Answer this FFA question using info from FFA.org: ${question}`}]
      })
    });
    const data = await response.json();
    return data.choices[0].message.content;
  }

  function fillTopic(topic) { document.getElementById("userInput").value = topic; }

  async function askAI() {
    const input = document.getElementById("userInput").value.trim();
    if (!input) return;
    const chatBox = document.getElementById("chatBox");

    const userMessage = document.createElement("p");
    userMessage.className = "user-msg";
    userMessage.innerHTML = `<strong>You:</strong> ${input}`;
    chatBox.appendChild(userMessage);

    const response = document.createElement("p");
    response.className = "ai-msg";
    response.innerHTML = `<strong>FFA AI:</strong> Loading...`;
    chatBox.appendChild(response);

    const answer = await askChatGPT(input);
    response.innerHTML = `<strong>FFA AI:</strong> ${answer}`;

    chatBox.scrollTop = chatBox.scrollHeight;
    document.getElementById("userInput").value = "";
  }

  // ===================== Chapter Messenger (Username login) =====================
  let loggedInUser = null;
  function loginUser() {
    const username = document.getElementById("usernameInput").value.trim();
    const status = document.getElementById("loginStatus");
    if(username.length < 1) { status.textContent="Please enter a valid username."; return; }
    loggedInUser = username;
    document.getElementById("loginDiv").style.display="none";
    document.getElementById("messengerDiv").style.display="block";
    status.textContent="";
    addSystemMessage(`✅ Logged in as ${loggedInUser}`);
  }

  const messages=[];
  function sendMessage() {
    const input=document.getElementById("msgInput").value.trim();
    if(!input || !loggedInUser) return;
    const msg={user:loggedInUser, text:input, time:new Date()};
    messages.push(msg);
    addMessage(msg);
    document.getElementById("msgInput").value="";
  }

  function addMessage(msg) {
    const msgBox=document.getElementById("msgBox");
    const p=document.createElement("p");
    p.innerHTML=`<strong>${msg.user}</strong> [${msg.time.toLocaleTimeString()}]: ${msg.text}`;
    msgBox.appendChild(p);
    msgBox.scrollTop=msgBox.scrollHeight;
  }

  function addSystemMessage(text) {
    const msgBox=document.getElementById("msgBox");
    const p=document.createElement("p");
    p.style.fontStyle="italic";
    p.style.color="var(--ffa-blue)";
    p.textContent=text;
    msgBox.appendChild(p);
    msgBox.scrollTop=msgBox.scrollHeight;
  }

  function clearMessages() {
    if(confirm("Clear all messages for this session?")) document.getElementById("msgBox").innerHTML="";
  }
</script>

</body>
</html>
