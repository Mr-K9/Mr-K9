<html>
 <head>
  <title>Chat Room | MPM</title>
  <style>
    body { 
      font-family: sans-serif; 
      padding: 20px; 
      background: #f0f0f0; 
      }
    #messages { 
      margin-top: 20px; 
      margin-bottom: 20px;
      padding: 10px; 
      background: #fff; 
      border-radius: 5px; 
      max-height: 400px; 
      overflow-y: auto; 
    }
    input { 
      padding: 8px; 
      width: 200px; 
      
    }
    button { 
      padding: 8px 12px; 
      
    }
    .message { 
      margin: 5px 0; 
      padding: 8px 12px; 
      border-radius: 6px; 
      }
    .me { 
      background: #ccf; 
      text-align: right; 
      
    }
    .other { 
      background: #eee; 
      
    }
    small { 
      color: #888; 
      font-size: 10px; 
      
    }
  </style>
</head>
<body>
<center>
 	<a href="https://www.xnxx.com"><img src="https://i.ibb.co/pjzD0sd/inbound980191521.png" /> </a>
<h1>Hi there 👋</h1>


<body>
  <h2>Chat room</h2>
  <div id="messages"></div>
  <input id="input" placeholder="Type message...">
  <button id="send">SEND</button>

 <script>
    let selfId = localStorage.getItem('selfId');
if (!selfId) {
  selfId = Math.random().toString(36).substring(2);
  localStorage.setItem('selfId', selfId);
}
const bc = new BroadcastChannel('my-chat');
const input = document.getElementById('input');
const sendBtn = document.getElementById('send');
const messages = document.getElementById('messages');

let chatData = JSON.parse(localStorage.getItem('chatData') || '[]');
chatData.forEach(m => addMessage(m.text, m.time, m.sender === selfId));

function addMessage(text, time, isMe) {
  const msg = document.createElement('div');
  msg.className = 'message ' + (isMe ? 'me' : 'other');
  msg.innerHTML = `<div>${text}</div><small>${isMe ? '👤 You' : '💬 Other'} • ${time}</small>`;
  messages.appendChild(msg);
  messages.scrollTop = messages.scrollHeight;
}

function saveMessage(text, time, sender) {
  chatData.push({ text, time, sender });
  localStorage.setItem('chatData', JSON.stringify(chatData));
}

sendBtn.addEventListener('click', () => {
  const text = input.value.trim();
  if (!text) return;
  const time = new Date().toLocaleTimeString();
  const msg = { text, time, sender: selfId };

  addMessage(text, time, true);
  saveMessage(text, time, selfId);
  bc.postMessage(msg);
  input.value = '';
});

bc.addEventListener('message', (e) => {
  const msg = e.data;
  if (msg.sender === selfId) return; // skip own echo
  addMessage(msg.text, msg.time, false);
  saveMessage(msg.text, msg.time, msg.sender);
});
</script>

</body>
</html>

<!--
**Mr-K9/Mr-K9** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
