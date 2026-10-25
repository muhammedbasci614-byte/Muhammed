
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GHOST CHAT</title>
<style>
:root {
  --bg: #08070d;
  --panel: #100d19;
  --panel2: #171123;
  --purple: #9b5cff;
  --purple2: #6d28d9;
  --text: #f5f0ff;
  --muted: #9c91ad;
  --border: #2c203e;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: Inter, system-ui, Arial, sans-serif;
}
button, input { font: inherit; }
button { cursor: pointer; }
.app {
  display: grid;
  grid-template-columns: 245px minmax(0,1fr);
  height: 100dvh;
  max-width: 1500px;
  margin: auto;
}
.sidebar {
  background: #0c0a12;
  border-right: 1px solid var(--border);
  padding: 22px 16px;
  display: flex;
  flex-direction: column;
  gap: 22px;
}
.logo {
  font-size: 24px;
  font-weight: 900;
  letter-spacing: 2px;
  color: white;
}
.logo span { color: var(--purple); }
.sub { color: var(--muted); font-size: 12px; margin-top: 5px; }
.section-title {
  color: var(--muted);
  font-size: 11px;
  letter-spacing: 1.5px;
  margin-bottom: 10px;
}
.channel {
  padding: 11px;
  border-radius: 9px;
  color: #cfc3df;
  background: var(--panel2);
}
.online-dot {
  display: inline-block;
  background: #55e6a5;
  width: 8px; height: 8px;
  border-radius: 50%;
  margin-right: 7px;
}
.profile {
  margin-top: auto;
  padding: 12px;
  border: 1px solid var(--border);
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 10px;
  overflow: hidden;
}
.avatar {
  width: 38px; height: 38px;
  display: grid; place-items: center;
  border-radius: 12px;
  background: linear-gradient(135deg,#a855f7,#4c1d95);
  font-weight: 800;
  flex-shrink: 0;
}
.small { font-size: 12px; color: var(--muted); }
.main {
  min-width: 0;
  display: flex;
  flex-direction: column;
}
.topbar {
  height: 72px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 0 24px;
  border-bottom: 1px solid var(--border);
  background: #0b0911;
}
.topbar h2 { font-size: 16px; margin: 0 0 4px; }
.status { color: #bca9d5; font-size: 12px; }
.pill {
  color: #d8c2ff;
  background: #201332;
  border: 1px solid #4d2d72;
  border-radius: 20px;
  padding: 7px 11px;
  font-size: 12px;
  white-space: nowrap;
}
.messages {
  flex: 1;
  overflow-y: auto;
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}
.welcome {
  text-align: center;
  padding: 22px 10px;
  border: 1px solid var(--border);
  background: radial-gradient(ellipse at top,#211334,#100d19 70%);
  border-radius: 16px;
}
.welcome .ghost { font-size: 32px; }
.welcome h1 { margin: 8px 0; font-size: 23px; }
.welcome p { color: var(--muted); font-size: 13px; margin: 0; }
.message { display: flex; gap: 11px; align-items: flex-start; }
.message .avatar { width: 35px; height: 35px; border-radius: 10px; }
.message-body { min-width: 0; }
.message-head { display: flex; align-items: center; gap: 9px; flex-wrap: wrap; }
.username { font-size: 13px; font-weight: 750; }
.time { font-size: 11px; color: var(--muted); }
.message-text {
  margin-top: 5px;
  line-height: 1.55;
  font-size: 14px;
  overflow-wrap: anywhere;
  white-space: pre-wrap;
}
.system {
  color: #bda1e9;
  font-size: 12px;
  text-align: center;
  padding: 5px;
}
.composer-wrap {
  padding: 12px 20px 18px;
  border-top: 1px solid var(--border);
  background: #0b0911;
}
.composer {
  display: flex;
  gap: 10px;
  padding: 8px;
  border: 1px solid #39274e;
  background: #15101f;
  border-radius: 13px;
}
.composer:focus-within { border-color: var(--purple); }
.composer input {
  min-width: 0;
  flex: 1;
  border: 0;
  outline: 0;
  color: white;
  background: transparent;
  padding: 8px;
}
.send {
  border: 0;
  border-radius: 9px;
  padding: 10px 16px;
  background: linear-gradient(135deg,#a855f7,#6d28d9);
  color: white;
  font-weight: 700;
}
.hint { color: var(--muted); font-size: 11px; margin: 9px 3px 0; }
#loginScreen {
  position: fixed; inset: 0; z-index: 10;
  display: grid; place-items: center;
  background: radial-gradient(ellipse at top,#211032,var(--bg) 65%);
  padding: 20px;
}
.login-card {
  width: min(390px,100%);
  padding: 28px;
  border: 1px solid #3a2454;
  border-radius: 20px;
  background: #100d19;
  box-shadow: 0 20px 80px #0009;
}
.login-card h1 { margin: 0; font-size: 28px; }
.login-card p { color: var(--muted); font-size: 13px; line-height: 1.6; }
.login-card input {
  width: 100%; margin: 12px 0;
  padding: 13px; border-radius: 10px;
  background: #09070e; color: white;
  border: 1px solid var(--border); outline: none;
}
.login-card button { width: 100%; padding: 13px; }
.hidden { display: none !important; }
@media(max-width:650px) {
  .app { grid-template-columns: 1fr; }
  .sidebar { display: none; }
  .topbar { height: 64px; padding: 0 15px; }
  .messages { padding: 15px; }
  .composer-wrap { padding: 10px; }
  .welcome h1 { font-size: 20px; }
  .pill { font-size: 10px; padding: 6px 8px; }
}
</style>
</head>
<body>

<div id="loginScreen">
  <div class="login-card">
    <div class="logo">GHOST<span> CHAT</span></div>
    <p>Gölgelere katıl. Kendi kullanıcı adını oluştur ve sohbete gir.</p>
    <input id="nameInput" maxlength="24" placeholder="Kullanıcı adın" autocomplete="nickname">
    <button class="send" onclick="login()">SOHBETE KATIL ↗</button>
    <p class="small">Bu sürüm yalnızca bu tarayıcıda çalışan demodur.</p>
  </div>
</div>

<div class="app">
  <aside class="sidebar">
    <div>
      <div class="logo">GHOST<span> CHAT</span></div>
      <div class="sub">PRIVATE • DARK • COMMUNITY</div>
    </div>
    <div>
      <div class="section-title">KANALLAR</div>
      <div class="channel"># genel-sohbet</div>
    </div>
    <div>
      <div class="section-title">TOPLULUK</div>
      <div class="small"><span class="online-dot"></span>Sen çevrimiçisin</div>
      <div class="small" style="margin-top:10px">Demo modu</div>
    </div>
    <div class="profile">
      <div class="avatar" id="sideAvatar">G</div>
      <div style="min-width:0">
        <div class="username" id="sideName">Misafir</div>
        <div class="small" id="userId">ID: —</div>
      </div>
    </div>
  </aside>

  <main class="main">
    <header class="topbar">
      <div>
        <h2># genel-sohbet</h2>
        <div class="status"><span class="online-dot"></span>GHOST CHAT topluluğu</div>
      </div>
      <div class="pill">✦ DARK MODE</div>
    </header>

    <section class="messages" id="messages">
      <div class="welcome">
        <div class="ghost">👻</div>
        <h1>GHOST CHAT'e hoş geldin</h1>
        <p>Karanlık tema. Mor detaylar. Yeni bir başlangıç.</p>
      </div>
    </section>

    <footer class="composer-wrap">
      <form class="composer" id="chatForm">
        <input id="messageInput" placeholder="Bir mesaj yaz veya /help kullan..." maxlength="1000" autocomplete="off">
        <button class="send" type="submit">Gönder</button>
      </form>
      <div class="hint">Komutları görmek için /help yaz.</div>
    </footer>
  </main>
</div>

<script>
const $ = id => document.getElementById(id);
let currentUser = "";
let currentId = "";
let muted = false;

function login() {
  const name = $("nameInput").value.trim().replace(/\s+/g, " ");
  if (!name) {
    $("nameInput").focus();
    return;
  }

  currentUser = name.slice(0, 24);

  // Demo kullanıcı ID'si: sunucu tarafından verilmez.
  let savedId = localStorage.getItem("ghost_demo_id");
  if (!savedId) {
    savedId = "G-" + Math.random().toString(36).slice(2, 9).toUpperCase();
    localStorage.setItem("ghost_demo_id", savedId);
  }
  currentId = savedId;

  $("sideName").textContent = currentUser;
  $("sideAvatar").textContent = currentUser[0].toUpperCase();
  $("userId").textContent = "ID: " + currentId;
  $("loginScreen").classList.add("hidden");
  $("messageInput").focus();

  addSystem(currentUser + " sohbete katıldı.");
  localStorage.setItem("ghost_demo_name", currentUser);
}

function addSystem(text) {
  const el = document.createElement("div");
  el.className = "system";
  el.textContent = text;
  $("messages").appendChild(el);
  scrollBottom();
}

function addMessage(name, text, own = false) {
  const row = document.createElement("div");
  row.className = "message";

  const avatar = document.createElement("div");
  avatar.className = "avatar";
  avatar.textContent = name[0].toUpperCase();

  const body = document.createElement("div");
  body.className = "message-body";

  const head = document.createElement("div");
  head.className = "message-head";

  const username = document.createElement("span");
  username.className = "username";
  username.textContent = name + (own ? " (sen)" : "");

  const time = document.createElement("span");
  time.className = "time";
  time.textContent = new Date().toLocaleTimeString("tr-TR", {
    hour: "2-digit", minute: "2-digit"
  });

  const messageText = document.createElement("div");
  messageText.className = "message-text";
  messageText.textContent = text;

  head.append(username, time);
  body.append(head, messageText);
  row.append(avatar, body);
  $("messages").appendChild(row);
  scrollBottom();
}

function scrollBottom() {
  $("messages").scrollTop = $("messages").scrollHeight;
}

function command(raw) {
  const parts = raw.trim().split(/\s+/);
  const cmd = parts[0].toLowerCase();

  switch (cmd) {
    case "/help":
      addSystem("Komutlar: /help, /nick İSİM, /me MESAJ, /clear, /id, /mute");
      addSystem("Ban, jail ve yetkili komutları için güvenli sunucu tarafı gerekir.");
      break;

    case "/nick": {
      const newName = parts.slice(1).join(" ").trim();
      if (!newName || newName.length > 24) {
        addSystem("Kullanım: /nick Yeniİsim");
        break;
      }
      currentUser = newName;
      $("sideName").textContent = newName;
      $("sideAvatar").textContent = newName[0].toUpperCase();
      localStorage.setItem("ghost_demo_name", newName);
      addSystem("Demo kullanıcı adın değiştirildi: " + newName);
      break;
    }

    case "/me":
      if (parts.length > 1) addMessage("* " + currentUser, parts.slice(1).join(" "), true);
      else addSystem("Kullanım: /me yaptığı şey");
      break;

    case "/clear":
      $("messages").replaceChildren();
      addSystem("Ekran temizlendi. Bu işlem yalnızca bu tarayıcıyı etkiler.");
      break;

    case "/id":
      addSystem("Demo kullanıcı ID'n: " + currentId);
      break;

    case "/mute":
      muted = !muted;
      addSystem(muted ? "Bu tarayıcıda mesaj gönderme kapatıldı." :
        "Bu tarayıcıda mesaj gönderme açıldı.");
      break;

    default:
      addSystem("Bilinmeyen komut. Komut listesi için /help yaz.");
  }
}

$("chatForm").addEventListener("submit", event => {
  event.preventDefault();
  const input = $("messageInput");
  const text = input.value.trim();

  if (!text) return;
  if (!currentUser) {
    addSystem("Önce kullanıcı adıyla giriş yap.");
    return;
  }
  if (muted) {
    addSystem("Mesaj gönderme bu tarayıcıda kapalı. /mute ile açabilirsin.");
    return;
  }

  input.value = "";
  if (text.startsWith("/")) command(text);
  else addMessage(currentUser, text, true);
});

$("nameInput").addEventListener("keydown", event => {
  if (event.key === "Enter") login();
});

const rememberedName = localStorage.getItem("ghost_demo_name");
if (rememberedName) $("nameInput").value = rememberedName;
</script>
</body>
</html>
