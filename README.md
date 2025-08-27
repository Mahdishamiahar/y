<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VIPZEXNET - چت هوش مصنوعی</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
:root {
    --bg-dark: #0d1117;
    --bg-darker: #090c13;
    --text-light: #fff;
    --text-lighter: #f0f6fc;
    --text-muted: #8b949e;
    --brand: #58a6ff;
    --brand-darker: #388bfd;
    --success: #238636;
    --success-darker: #2ea043;
    --card-dark: rgba(33,38,45,0.9);
    --card-darker: rgba(28,32,38,0.95);
    --border-color: #30363d;
    --user-msg: #1c532c;
    --bot-msg: #1f2937;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: var(--bg-dark);
    color: var(--text-light);
    display: flex;
    flex-direction: column;
    height: 100vh;
    position: relative;
    overflow: hidden;
}

.background-text {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 42px;
    font-weight: bold;
    color: rgba(255, 255, 255, 0.05);
    user-select: none;
    pointer-events: none;
    z-index: 0;
    text-align: center;
    line-height: 1.6;
    max-width: 90%;
    text-shadow: 0px 0px 15px rgba(255, 255, 255, 0.1);
}

.gradient-bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(125deg, var(--bg-darker) 0%, var(--bg-dark) 30%, #0d2b47 70%, #093d69 100%);
    z-index: -1;
    opacity: 0.8;
}

header {
    background: rgba(22, 27, 34, 0.95);
    padding: 12px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--border-color);
    font-size: 16px;
    z-index: 10;
    position: relative;
    backdrop-filter: blur(10px);
    box-shadow: 0 2px 15px rgba(0, 0, 0, 0.2);
}

header h1 {
    margin: 0;
    font-size: 18px;
    color: var(--brand);
    flex: 1;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    display: flex;
    align-items: center;
    gap: 8px;
}

.header-actions {
    display: flex;
    align-items: center;
    gap: 10px;
}

#chatWindow {
    flex: 1;
    overflow-y: auto;
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    z-index: 1;
    position: relative;
    scroll-behavior: smooth;
}

#chatWindow::-webkit-scrollbar {
    width: 8px;
}

#chatWindow::-webkit-scrollbar-track {
    background: rgba(13, 17, 23, 0.5);
    border-radius: 4px;
}

#chatWindow::-webkit-scrollbar-thumb {
    background: var(--border-color);
    border-radius: 4px;
}

#chatWindow::-webkit-scrollbar-thumb:hover {
    background: #484f58;
}

.welcome-container {
    background: var(--card-dark);
    border-radius: 16px;
    padding: 20px;
    margin: 10px 0 20px;
    text-align: center;
    border: 1px solid var(--border-color);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.welcome-container h2 {
    color: var(--brand);
    margin-bottom: 12px;
    font-size: 20px;
}

.welcome-container p {
    color: var(--text-muted);
    line-height: 1.6;
    margin-bottom: 15px;
}

.suggestion-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
    margin-top: 15px;
}

.chip {
    background: rgba(88, 166, 255, 0.15);
    color: var(--brand);
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.2s ease;
    border: 1px solid rgba(88, 166, 255, 0.3);
}

.chip:hover {
    background: rgba(88, 166, 255, 0.25);
    transform: translateY(-2px);
}

.message {
    max-width: 85%;
    padding: 12px 16px;
    border-radius: 16px;
    line-height: 1.5;
    white-space: pre-wrap;
    position: relative;
    animation: fadeIn 0.3s ease-in-out;
    word-break: break-word;
    font-size: 15px;
    display: flex;
    align-items: flex-start;
    gap: 10px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.user {
    background: var(--user-msg);
    color: var(--text-lighter);
    align-self: flex-end;
    border-bottom-right-radius: 4px;
}

.bot {
    background: var(--bot-msg);
    color: var(--text-lighter);
    align-self: flex-start;
    border-bottom-left-radius: 4px;
}

.msg-time {
    font-size: 11px;
    opacity: 0.7;
    text-align: left;
    margin-top: 6px;
    direction: ltr;
}

.msg-user {
    font-weight: bold;
    font-size: 13px;
    margin-bottom: 4px;
    color: var(--brand);
}

#inputArea {
    display: flex;
    padding: 12px 16px;
    border-top: 1px solid var(--border-color);
    background: rgba(22, 27, 34, 0.95);
    gap: 10px;
    align-items: center;
    z-index: 10;
    position: relative;
    backdrop-filter: blur(10px);
}

#userInput {
    flex: 1;
    padding: 12px 16px;
    border: 1px solid var(--border-color);
    border-radius: 12px;
    background: var(--card-darker);
    color: var(--text-light);
    font-size: 15px;
    outline: none;
    transition: all 0.2s ease;
}

#userInput:focus {
    border-color: var(--brand);
    box-shadow: 0 0 0 2px rgba(88, 166, 255, 0.2);
}

#sendBtn, #uploadBtn {
    padding: 12px 16px;
    background: var(--brand);
    border: none;
    border-radius: 12px;
    cursor: pointer;
    color: #fff;
    font-size: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s ease;
}

#sendBtn:hover, #uploadBtn:hover {
    background: var(--brand-darker);
    transform: translateY(-1px);
}

#sendBtn:active, #uploadBtn:active {
    transform: translateY(0);
}

#historyMenu {
    display: none;
    position: absolute;
    top: 100%;
    right: 0;
    background: var(--card-dark);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    width: 280px;
    z-index: 100;
    max-height: 350px;
    overflow-y: auto;
    font-size: 14px;
    margin-top: 8px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    backdrop-filter: blur(10px);
}

#historyMenu button {
    width: 100%;
    padding: 10px 14px;
    border: none;
    background: none;
    color: var(--text-light);
    text-align: right;
    cursor: pointer;
    font-size: 14px;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: all 0.2s ease;
    border-bottom: 1px solid rgba(48, 54, 61, 0.3);
}

#historyMenu button:last-child {
    border-bottom: none;
}

#historyMenu button:hover {
    background: rgba(88, 166, 255, 0.1);
}

#menuContainer {
    position: relative;
    z-index: 1;
}

#profileModal {
    display: none;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: var(--card-dark);
    border: 1px solid var(--border-color);
    border-radius: 16px;
    padding: 20px;
    z-index: 200;
    width: 90%;
    max-width: 400px;
    color: var(--text-light);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
    backdrop-filter: blur(10px);
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border-color);
}

.modal-header h3 {
    color: var(--brand);
    font-size: 18px;
}

#closeProfile {
    background: none;
    border: none;
    color: var(--text-muted);
    font-size: 20px;
    cursor: pointer;
    transition: all 0.2s;
}

#closeProfile:hover {
    color: var(--text-light);
}

#profileModal label {
    display: block;
    margin-bottom: 6px;
    color: var(--text-muted);
    font-size: 14px;
}

#profileModal input {
    width: 100%;
    margin-bottom: 16px;
    padding: 10px 12px;
    background: var(--bg-dark);
    color: var(--text-light);
    border: 1px solid var(--border-color);
    border-radius: 8px;
    font-size: 14px;
    outline: none;
    transition: all 0.2s;
}

#profileModal input:focus {
    border-color: var(--brand);
    box-shadow: 0 0 0 2px rgba(88, 166, 255, 0.2);
}

.modal-footer {
    display: flex;
    justify-content: flex-end;
    gap: 10px;
    margin-top: 10px;
}

#saveProfile {
    background: var(--success);
    color: #fff;
    padding: 8px 16px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    transition: all 0.2s;
}

#saveProfile:hover {
    background: var(--success-darker);
}

.typing {
    font-style: italic;
    opacity: 0.7;
}

.typing-dots {
    display: inline-flex;
    align-items: center;
    gap: 3px;
}

.typing-dots span {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background-color: var(--text-muted);
    animation: typingAnimation 1.4s infinite ease-in-out;
}

.typing-dots span:nth-child(1) { animation-delay: 0s; }
.typing-dots span:nth-child(2) { animation-delay: 0.2s; }
.typing-dots span:nth-child(3) { animation-delay: 0.4s; }

.message img.avatar {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    object-fit: cover;
    flex-shrink: 0;
}

.message img.attachment {
    max-width: 100%;
    border-radius: 12px;
    margin-top: 8px;
    border: 1px solid var(--border-color);
}

.model-selector {
    display: flex;
    align-items: center;
    gap: 8px;
    color: var(--text-muted);
    font-size: 13px;
    margin-left: 15px;
}

.model-selector select {
    background: var(--bg-dark);
    color: var(--text-light);
    border: 1px solid var(--border-color);
    border-radius: 6px;
    padding: 4px 8px;
    font-size: 13px;
    outline: none;
    cursor: pointer;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

@keyframes typingAnimation {
    0%, 100% { transform: scale(0.8); opacity: 0.5; }
    50% { transform: scale(1.2); opacity: 1; }
}

@media (max-width: 768px) {
    .background-text {
        font-size: 28px;
    }
    
    .message {
        max-width: 90%;
        font-size: 14px;
    }
    
    header h1 {
        font-size: 16px;
    }
    
    .header-actions {
        gap: 5px;
    }
    
    .model-selector {
        display: none;
    }
    
    #historyMenu {
        width: 250px;
    }
}

.notification {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: var(--success);
    color: white;
    padding: 12px 20px;
    border-radius: 12px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    z-index: 1000;
    animation: slideIn 0.3s ease-out;
    display: flex;
    align-items: center;
    gap: 10px;
}

@keyframes slideIn {
    from { transform: translateX(100px); opacity: 0; }
    to { transform: translateX(0); opacity: 1; }
}
</style>
</head>
<body>

<div class="gradient-bg"></div>
<div class="background-text">من Al VIPZEXNET هستم<br><span style="font-size: 30px;">چگونه می توانم امروز به شما کمک کنم</span></div>

<header>
  <h1><i class="fas fa-robot"></i> VIPZEXNET</h1>
  <div class="header-actions">
    <div class="model-selector">
      <span>مدل:</span>
      <select id="modelSelect">
        <option value="openai-large">GPT-4</option>
        <option value="openai-medium">GPT-3.5</option>
        <option value="claude">Claude</option>
        <option value="llama">Llama 2</option>
      </select>
    </div>
    <div id="menuContainer">
      <button id="menuBtn" title="منو"><i class="fas fa-ellipsis-v"></i></button>
      <div id="historyMenu">
        <button id="newChat"><i class="fas fa-plus"></i> چت جدید</button>
        <button id="profileBtn"><i class="fas fa-user"></i> پروفایل</button>
        <button id="clearHistoryBtn"><i class="fas fa-trash"></i> پاک کردن تاریخچه</button>
        <button id="exportBtn"><i class="fas fa-download"></i> ذخیره چت</button>
        <div id="chatHistoryList"></div>
      </div>
    </div>
  </div>
</header>

<div id="chatWindow">
  <div class="welcome-container">
    <h2>به VIPZEXNET خوش آمدید!</h2>
    <p>من یک دستیار هوش مصنوعی هستم که می‌توانم به سوالات شما پاسخ دهم، در حل مشکلات کمک کنم و با شما گفتگو کنم.</p>
    <div class="suggestion-chips">
      <div class="chip" data-prompt="هوش مصنوعی چیست؟">هوش مصنوعی چیست؟</div>
      <div class="chip" data-prompt="چگونه می توانم کدنویسی یاد بگیرم؟">یادگیری کدنویسی</div>
      <div class="chip" data-prompt="اتوماسیون چیست و چه کاربردی دارد؟">اتوماسیون چیست؟</div>
      <div class="chip" data-prompt="تکنولوژی بلاکچین را توضیح بده">بلاکچین چیست؟</div>
    </div>
  </div>
</div>

<div id="inputArea">
  <button id="uploadBtn" title="افزودن فایل"><i class="fas fa-paperclip"></i></button>
  <input type="text" id="userInput" placeholder="پیام خود را بنویسید..." onkeydown="if(event.key==='Enter'){sendMessage()}">
  <button id="sendBtn" onclick="sendMessage()"><i class="fas fa-paper-plane"></i></button>
</div>

<div id="profileModal">
  <div class="modal-header">
    <h3>پروفایل کاربری</h3>
    <button id="closeProfile"><i class="fas fa-times"></i></button>
  </div>
  <label>نام:</label>
  <input type="text" id="profileName" placeholder="نام خود را وارد کنید">
  <label>ایمیل:</label>
  <input type="email" id="profileEmail" placeholder="ایمیل خود را وارد کنید">
  <label>عکس پروفایل:</label>
  <input type="file" id="profileAvatar" accept="image/*">
  <div class="modal-footer">
    <button id="saveProfile"><i class="fas fa-save"></i> ذخیره</button>
  </div>
</div>

<input type="file" id="fileInput" style="display:none" accept="image/*,.txt,.pdf,.doc,.docx">

<script>
// متغیرهای全局
let selectedModel = "openai-large";
const chatWindow = document.getElementById("chatWindow");
const userInput = document.getElementById("userInput");
const modelSelect = document.getElementById("modelSelect");
let currentChatId = "default";

// مقداردهی اولیه
document.addEventListener("DOMContentLoaded", function() {
  loadChatHistory();
  loadUserProfile();
  setupEventListeners();
  
  // تنظیم مدل انتخابی
  modelSelect.value = selectedModel;
  modelSelect.addEventListener("change", () => {
    selectedModel = modelSelect.value;
    showNotification(`مدل به ${modelSelect.options[modelSelect.selectedIndex].text} تغییر کرد`);
  });
});

// بارگذاری تاریخچه چت
function loadChatHistory() {
  const history = JSON.parse(localStorage.getItem(`chatHistory_${currentChatId}`) || "[]");
  chatWindow.innerHTML = '';
  
  // اضافه کردن welcome message
  const welcomeMsg = document.querySelector('.welcome-container');
  if (welcomeMsg) {
    chatWindow.appendChild(welcomeMsg);
  }
  
  history.forEach(msg => {
    addMessage(msg.text, msg.sender, false, msg.time, msg.name, msg.img);
  });
  
  // اضافه کردن event listeners برای chips
  document.querySelectorAll('.chip').forEach(chip => {
    chip.addEventListener('click', () => {
      userInput.value = chip.getAttribute('data-prompt');
      sendMessage();
    });
  });
}

// ذخیره پیام در تاریخچه
function saveMessage(text, sender, time, name = null, img = null) {
  const history = JSON.parse(localStorage.getItem(`chatHistory_${currentChatId}`) || "[]");
  history.push({ text, sender, time, name, img });
  localStorage.setItem(`chatHistory_${currentChatId}`, JSON.stringify(history));
}

// افزودن پیام به چت
function addMessage(text, sender, save = true, time = null, name = null, img = null, isTyping = false) {
  const msgDiv = document.createElement("div");
  msgDiv.className = `message ${sender}`;
  
  if (!time) time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
  
  let profile = JSON.parse(localStorage.getItem("userProfile") || "{}");
  let userDisplay = name ? `<div class="msg-user">${name}</div>` : "";
  
  let avatarTag = "";
  if (sender === "user" && profile.avatar) {
    avatarTag = `<img src="${profile.avatar}" class="avatar">`;
  } else if (sender === "bot") {
    avatarTag = `<img src="https://api.dicebear.com/6.x/bottts-neutral/svg?seed=VIPZEXNET" class="avatar">`;
  }
  
  let imgTag = img ? `<img src="${img}" class="attachment">` : "";
  
  let messageContent = text;
  if (isTyping) {
    messageContent = `<div class="typing-dots"><span></span><span></span><span></span></div>`;
  }
  
  msgDiv.innerHTML = `
    ${avatarTag}
    <div style="flex:1">
      ${userDisplay}
      <span>${messageContent}</span>
      ${imgTag}
      <div class="msg-time">${time}</div>
    </div>
  `;
  
  chatWindow.appendChild(msgDiv);
  chatWindow.scrollTop = chatWindow.scrollHeight;
  
  if (save) saveMessage(text, sender, time, name, img);
  
  // امکان ویرایش پیام با دابل کلیک
  if (sender === "user") {
    msgDiv.addEventListener('dblclick', () => {
      const newText = prompt("ویرایش پیام:", text);
      if (newText !== null) {
        msgDiv.querySelector("span").textContent = newText;
        updateMessageInHistory(text, newText);
      }
    });
  }
  
  return msgDiv;
}

// به روزرسانی پیام در تاریخچه
function updateMessageInHistory(oldText, newText) {
  const history = JSON.parse(localStorage.getItem(`chatHistory_${currentChatId}`) || "[]");
  const msg = history.find(m => m.text === oldText && m.sender === "user");
  if (msg) {
    msg.text = newText;
    localStorage.setItem(`chatHistory_${currentChatId}`, JSON.stringify(history));
  }
}

// ارسال پیام
async function sendMessage() {
  const text = userInput.value.trim();
  if (!text) return;
  
  const profile = JSON.parse(localStorage.getItem("userProfile") || "{}");
  addMessage(text, "user", true, null, profile.name || "شما");
  userInput.value = "";
  
  const loadingMsg = addMessage("در حال پردازش درخواست شما...", "bot", false, null, null, null, true);
  
  try {
    // شبیه‌سازی تاخیر برای پاسخ
    setTimeout(async () => {
      try {
        // در اینجا می‌توانید از API واقعی استفاده کنید
        // const response = await fetch(`https://api.example.com/chat?model=${selectedModel}&prompt=${encodeURIComponent(text)}`);
        // const data = await response.json();
        
        // پاسخ شبیه‌سازی شده
        const responses = {
          "openai-large": "این یک پاسخ از مدل GPT-4 است. من می‌توانم به سوالات پیچیده پاسخ دهم و مسائل مختلف را حل کنم.",
          "openai-medium": "این پاسخ از مدل GPT-3.5 است. من می‌توانم به بسیاری از سوالات شما پاسخ دهم.",
          "claude": "این پاسخ از مدل Claude است. من بر روی مکالمات طبیعی و درک عمیق متن تخصص دارم.",
          "llama": "این پاسخ از مدل Llama 2 است. من یک مدل متن باز با قابلیت‌های پیشرفته هستم."
        };
        
        const responseText = responses[selectedModel] || "من یک دستیار هوش مصنوعی هستم و می‌توانم به شما کمک کنم. لطفاً سوال خود را بپرسید.";
        
        loadingMsg.remove();
        addMessage(responseText, "bot");
      } catch (err) {
        loadingMsg.remove();
        addMessage("❌ خطا در دریافت پاسخ از سرور", "bot");
        console.error(err);
      }
    }, 1500);
  } catch (err) {
    loadingMsg.remove();
    addMessage("❌ خطا در ارسال درخواست", "bot");
    console.error(err);
  }
}

// مدیریت آپلود فایل
function setupFileUpload() {
  const uploadBtn = document.getElementById("uploadBtn");
  const fileInput = document.getElementById("fileInput");
  
  uploadBtn.addEventListener("click", () => fileInput.click());
  
  fileInput.addEventListener("change", (e) => {
    const file = e.target.files[0];
    if (!file) return;
    
    const reader = new FileReader();
    reader.onload = function() {
      const profile = JSON.parse(localStorage.getItem("userProfile") || "{}");
      
      if (file.type.startsWith("image/")) {
        addMessage("تصویر ارسال شده", "user", true, null, profile.name || "شما", reader.result);
      } else if (file.type === "text/plain") {
        addMessage(`فایل متنی: ${file.name}\n${reader.result}`, "user");
      } else {
        addMessage(`فایل ارسال شده: ${file.name}`, "user");
      }
    };
    reader.readAsDataURL(file);
    
    // reset file input
    fileInput.value = "";
  });
}

// مدیریت منو و تاریخچه
function setupMenu() {
  const menuBtn = document.getElementById("menuBtn");
  const historyMenu = document.getElementById("historyMenu");
  const chatHistoryList = document.getElementById("chatHistoryList");
  const newChatBtn = document.getElementById("newChat");
  const clearHistoryBtn = document.getElementById("clearHistoryBtn");
  const exportBtn = document.getElementById("exportBtn");
  
  menuBtn.addEventListener("click", (e) => {
    e.stopPropagation();
    historyMenu.style.display = historyMenu.style.display === "block" ? "none" : "block";
    renderHistoryList();
  });
  
  newChatBtn.addEventListener("click", () => {
    if (confirm("آیا مطمئن هستید که می‌خواهید یک چت جدید شروع کنید؟")) {
      currentChatId = Date.now().toString();
      localStorage.setItem("currentChatId", currentChatId);
      chatWindow.innerHTML = '';
      loadChatHistory();
      historyMenu.style.display = "none";
      showNotification("چت جدید شروع شد");
    }
  });
  
  clearHistoryBtn.addEventListener("click", () => {
    if (confirm("آیا مطمئن هستید که می‌خواهید تمام تاریخچه چت پاک شود؟")) {
      localStorage.removeItem(`chatHistory_${currentChatId}`);
      chatWindow.innerHTML = '';
      loadChatHistory();
      historyMenu.style.display = "none";
      showNotification("تاریخچه چت پاک شد");
    }
  });
  
  exportBtn.addEventListener("click", () => {
    const history = JSON.parse(localStorage.getItem(`chatHistory_${currentChatId}`) || "[]");
    const chatText = history.map(msg => `${msg.sender === 'user' ? 'شما' : 'ربات'}: ${msg.text}`).join('\n\n');
    
    const blob = new Blob([chatText], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `vipzexnet-chat-${new Date().toLocaleDateString('fa-IR')}.txt`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
    
    historyMenu.style.display = "none";
    showNotification("چت با موفقیت ذخیره شد");
  });
  
  // بستن منو با کلیک خارج از آن
  document.addEventListener("click", (e) => {
    if (!historyMenu.contains(e.target) && e.target !== menuBtn) {
      historyMenu.style.display = "none";
    }
  });
}

// نمایش لیست تاریخچه
function renderHistoryList() {
  const history = JSON.parse(localStorage.getItem(`chatHistory_${currentChatId}`) || "[]");
  chatHistoryList.innerHTML = "";
  
  if (history.length === 0) {
    const emptyMsg = document.createElement("div");
    emptyMsg.style.padding = "10px";
    emptyMsg.style.color = "var(--text-muted)";
    emptyMsg.style.textAlign = "center";
    emptyMsg.textContent = "تاریخچه‌ای وجود ندارد";
    chatHistoryList.appendChild(emptyMsg);
    return;
  }
  
  history.forEach((msg, index) => {
    if (index > 9) return; // فقط 10 آیتم آخر نمایش داده شود
    
    const btn = document.createElement("button");
    btn.innerHTML = `${msg.sender === "user" ? "<i class='fas fa-user'></i>" : "<i class='fas fa-robot'></i>"} ${msg.text.slice(0, 30)}${msg.text.length > 30 ? "..." : ""}`;
    
    btn.addEventListener("click", () => {
      alert(`پیام کامل:\n\n${msg.text}\n\nزمان: ${msg.time}`);
    });
    
    chatHistoryList.appendChild(btn);
  });
}

// مدیریت پروفایل کاربر
function setupProfile() {
  const profileBtn = document.getElementById("profileBtn");
  const profileModal = document.getElementById("profileModal");
  const closeProfile = document.getElementById("closeProfile");
  const saveProfile = document.getElementById("saveProfile");
  const profileName = document.getElementById("profileName");
  const profileEmail = document.getElementById("profileEmail");
  const profileAvatar = document.getElementById("profileAvatar");
  
  profileBtn.addEventListener("click", () => {
    profileModal.style.display = "block";
    const profile = JSON.parse(localStorage.getItem("userProfile") || "{}");
    profileName.value = profile.name || "";
    profileEmail.value = profile.email || "";
  });
  
  closeProfile.addEventListener("click", () => {
    profileModal.style.display = "none";
  });
  
  saveProfile.addEventListener("click", () => {
    const profile = {
      name: profileName.value.trim(),
      email: profileEmail.value.trim()
    };
    
    if (profileAvatar.files[0]) {
      const reader = new FileReader();
      reader.onload = function() {
        profile.avatar = reader.result;
        localStorage.setItem("userProfile", JSON.stringify(profile));
        showNotification("پروفایل با موفقیت ذخیره شد");
        profileModal.style.display = "none";
      };
      reader.readAsDataURL(profileAvatar.files[0]);
    } else {
      const oldProfile = JSON.parse(localStorage.getItem("userProfile") || "{}");
      if (oldProfile.avatar) profile.avatar = oldProfile.avatar;
      localStorage.setItem("userProfile", JSON.stringify(profile));
      showNotification("پروفایل با موفقیت ذخیره شد");
      profileModal.style.display = "none";
    }
  });
  
  // بستن مودال با کلیک خارج از آن
  profileModal.addEventListener("click", (e) => {
    if (e.target === profileModal) {
      profileModal.style.display = "none";
    }
  });
}

// بارگذاری پروفایل کاربر
function loadUserProfile() {
  const profile = JSON.parse(localStorage.getItem("userProfile") || "{}");
  if (!profile.name) {
    // اگر پروفایل وجود ندارد، پس از 2 ثانیه مودال پروفایل نمایش داده شود
    setTimeout(() => {
      document.getElementById("profileModal").style.display = "block";
    }, 2000);
  }
}

// نمایش نوتیفیکیشن
function showNotification(message) {
  const notification = document.createElement("div");
  notification.className = "notification";
  notification.innerHTML = `<i class="fas fa-check-circle"></i> ${message}`;
  
  document.body.appendChild(notification);
  
  setTimeout(() => {
    notification.remove();
  }, 3000);
}

// تنظیم کلیه event listeners
function setupEventListeners() {
  setupFileUpload();
  setupMenu();
  setupProfile();
  
  // بستن مودال پروفایل با کلید ESC
  document.addEventListener("keydown", (e) => {
    if (e.key === "Escape") {
      document.getElementById("profileModal").style.display = "none";
      document.getElementById("historyMenu").style.display = "none";
    }
  });
}
</script>
</body>
</html>
