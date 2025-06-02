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

      const apiKey = "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"; // <== 把这里换成你自己的

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
