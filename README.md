<!DOCTYPE html>
<html>
<head>
  <title>AI 聊天客服</title>
  <style>
    body { font-family: sans-serif; text-align: center; padding: 40px; }
    #response { margin-top: 20px; white-space: pre-wrap; }
  </style>
</head>
<body>
  <h1>欢迎来到 AI 客服</h1>
  <input id="question" type="text" placeholder="请输入你的问题..." size="50">
  <button onclick="ask()">发送</button>
  <div id="response"></div>

  <script>
    async function ask() {
      const question = document.getElementById('question').value;
      const responseDiv = document.getElementById('response');
      responseDiv.innerText = "思考中...";

      const apiKey = "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"; //  

      const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${apiKey}`
        },
        body: JSON.stringify({
          model: "gpt-3.5-turbo",
          messages: [{ role: "user", content: question }]
        })
      });

      const data = await response.json();
      responseDiv.innerText = data.choices?.[0]?.message?.content || "出错了";
    }
  </script>
</body>
</html>
