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

<script>
  // ===================== Chapter Messenger (Username login) =====================
  let loggedInUser = null;

  function loginUser() {
    const username = document.getElementById("usernameInput").value.trim();
    const status = document.getElementById("loginStatus");

    if(username.length < 1) {
      status.textContent = "Please enter a valid username.";
      return;
    }

    loggedInUser = username;
    document.getElementById("loginDiv").style.display = "none";
    document.getElementById("messengerDiv").style.display = "block";
    status.textContent = "";
    addSystemMessage(`✅ Logged in as ${loggedInUser}`);
  }

  const messages = [];

  function sendMessage() {
    const input = document.getElementById("msgInput").value.trim();
    if(!input || !loggedInUser) return;

    const msg = {user: loggedInUser, text: input, time: new Date()};
    messages.push(msg);
    addMessage(msg);
    document.getElementById("msgInput").value = "";
  }

  function addMessage(msg) {
    const msgBox = document.getElementById("msgBox");
    const p = document.createElement("p");
    p.innerHTML = `<strong>${msg.user}</strong> [${msg.time.toLocaleTimeString()}]: ${msg.text}`;
    msgBox.appendChild(p);
    msgBox.scrollTop = msgBox.scrollHeight;
  }

  function addSystemMessage(text) {
    const msgBox = document.getElementById("msgBox");
    const p = document.createElement("p");
    p.style.fontStyle = "italic";
    p.style.color = "var(--ffa-blue)";
    p.textContent = text;
    msgBox.appendChild(p);
    msgBox.scrollTop = msgBox.scrollHeight;
  }

  function clearMessages() {
    if(confirm("Clear all messages for this session?")) {
      document.getElementById("msgBox").innerHTML = "";
    }
  }
</script>
