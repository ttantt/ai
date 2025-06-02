<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>AI 聊天客服</title>
  <style>
    body { font-family: sans-serif; text-align: center; background: #f0f0f0; padding: 30px; }
    #chat { width: 90%; max-width: 500px; margin: auto; background: white; padding: 20px; border-radius: 10px; }
    #output { margin-top: 20px; text-align: left; background: #eef; padding: 10px; border-radius: 5px; }
  </style>
</head>
<body>
  <div id="chat">
    <h2>欢迎来到 AI 客服</h2>
    <p>请问你想了解什么？</p >
    <input type="text" id="question" placeholder="请输入问题">
    <button onclick="askAI()">发送</button>
    <div id="output"></div>
  </div>

  <script>
    async function askAI() {
      const q = document.getElementById('question').value;
      const responseBox = document.getElementById('output');
      responseBox.innerHTML = "AI 正在思考中...";

      const apiKey = "你的API密钥"; // 下一步教你去拿！
      const res = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": "Bearer " + apiKey
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: [{ role: "user", content: q }]
        })
      });

      const data = await res.json();
      responseBox.innerHTML = "<b>AI：</b>" + data.choices[0].message.content;
    }
  </script>
</body>
</html>
