<!DOCTYPE html>
<html lang="ku">
<head>
  <meta charset="UTF-8">
  <title>قوتابخانەی دواڕۆژی ناحکومی</title>
  <style>
    body {
      background-color: #f0f0f0;
      font-family: Arial, sans-serif;
      padding: 30px;
    }
    form {
      background-color: #fff;
      padding: 20px;
      max-width: 500px;
      margin: auto;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      border-radius: 8px;
    }
    .logo-container {
      text-align: center;
      margin-bottom: 20px;
    }
    .logo-container img {
      width: 120px;
      height: auto;
    }
    h2 {
      text-align: center;
      color: blue;
      margin-bottom: 20px;
    }
    input, textarea {
      width: 100%;
      margin: 10px 0;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 16px;
    }
    button {
      background-color: blue;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      width: 100%;
      font-size: 16px;
    }
    button:hover {
      background-color: #218838;
    }
  </style>
</head>
<body>

<form id="telegramForm">
  <div class="logo-container">
    <img src="dr.png" alt="Logo"> <!-- 🔁 Replace with your actual logo path -->
  </div>
  <h2>قوتابخانەی دواڕۆژی ناحکومی</h2>

  ناو <input type="text" id="name" placeholder="ناو " required lang="ku" dir="auto" />
  ژمارەی مۆبایل<input type="text" id="score" placeholder="ژمارەی مۆبایل" required />
  رۆژی لە دایکبوون <input type="date" id="dob" required /><br>
  ناوی ئەو قوتابخانەی لێوەی هاتووی<textarea id="feedback" placeholder="" rows="5" required lang="ku" dir="auto"></textarea>

  <button type="submit">ناردن </button>
</form>

<script>
  const TOKEN = "8302380004:AAHELl8WHAoP3Em6PC231roCi_QTlxr5Ayc";
  const CHAT_ID = "1881744939";
  const TELEGRAM_API_URL = `https://api.telegram.org/bot${TOKEN}/sendMessage`;

  // Send to Telegram
  function sendToTelegram(message, resetForm = false) {
    fetch(TELEGRAM_API_URL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        chat_id: CHAT_ID,
        text: message
      })
    })
    .then(response => {
      if (response.ok) {
        if (resetForm) {
          alert("✅ زانیاریەکان بە سەرکەوتووی نێردران");
          document.getElementById("telegramForm").reset();
        }
      } else {
        alert("❌ نەتوانرا زانیاری بنێردرێت.");
      }
    })
    .catch(err => {
      console.error("Fetch error:", err);
      alert("⚠️ هەڵەیەک ڕوویدا لە نێردنی زانیاری.");
    });
  }

  // Form submit
  document.getElementById("telegramForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const name = document.getElementById("name").value;
    const score = document.getElementById("score").value;
    const dob = document.getElementById("dob").value;
    const feedback = document.getElementById("feedback").value;

    const message = `📥 زانیارییەکانی بەکارهێنەر:\n\n👤 ناو: ${name}\n📞 ژمارەی مۆبایل: ${score}\n🎂 بەرواری لەدایکبوون: ${dob}\n🏫 ناوی قوتابخانەی لێوەی هاتووە:\n${feedback}`;
    sendToTelegram(message, true);
  });

  // Global error handler
  window.onerror = function(message, source, lineno, colno, error) {
    const errorMessage = `🚨 هەڵەیەک ڕوویدا:\n📝 پەیام: ${message}\n📄 فایل: ${source}\n📍 هێڵ: ${lineno}, ستوون: ${colno}\n🔍 زانیاری زیاتر: ${error}`;
    sendToTelegram(errorMessage);
    alert("⚠️ هەڵەیەک ڕوویدا، تکایە دواتر هەوڵ بدە.");
  };
</script>

</body>
</html>
