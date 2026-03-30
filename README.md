<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hadi Pro AI 🤖</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #0f172a; color: white; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
        .chat-container { width: 90%; max-width: 500px; background: #1e293b; padding: 20px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        h2 { text-align: center; color: #38bdf8; }
        #chat-box { height: 300px; overflow-y: auto; border: 1px solid #334155; padding: 10px; margin-bottom: 10px; border-radius: 10px; background: #0f172a; }
        .user-msg { color: #facc15; margin: 5px 0; }
        .ai-msg { color: #38bdf8; margin: 5px 0; padding-bottom: 10px; border-bottom: 1px solid #334155; }
        input { width: 75%; padding: 10px; border-radius: 5px; border: none; outline: none; }
        button { width: 20%; padding: 10px; background: #38bdf8; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body>

<div class="chat-container">
    <h2>Hadi Pro AI 🤖</h2>
    <div id="chat-box"></div>
    <input type="text" id="userInput" placeholder="Kuch bhi pucho...">
    <button onclick="askAI()">Send</button>
</div>

<script>
    const API_KEY = "YAHAN_APNI_API_KEY_PASTE_KAREIN"; // <-- Apni Key Yahan Dalein

    async function askAI() {
        const input = document.getElementById("userInput");
        const chatBox = document.getElementById("chat-box");
        if(!input.value) return;

        chatBox.innerHTML += `<div class="user-msg"><b>Aap:</b> ${input.value}</div>`;
        const prompt = input.value;
        input.value = "";

        try {
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${API_KEY}`, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
            });
            const data = await response.json();
            const aiText = data.candidates[0].content.parts[0].text;
            chatBox.innerHTML += `<div class="ai-msg"><b>Hadi AI:</b> ${aiText}</div>`;
        } catch (error) {
            chatBox.innerHTML += `<div class="ai-msg" style="color:red;">Error: API Key check karein!</div>`;
        }
        chatBox.scrollTop = chatBox.scrollHeight;
    }
</script>

</body>
</html>
