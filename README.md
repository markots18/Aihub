<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Hub</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>AI Tool Hub</h1>
    <textarea id="userInput" placeholder="Enter your text here..."></textarea>
    <div class="buttons">
      <button onclick="useOpenAI()">OpenAI</button>
      <button onclick="useHuggingFace()">Hugging Face</button>
      <button onclick="useCustomAI()">Custom AI</button>
    </div>
    <div id="result"></div>
  </div>
  <script src="app.js"></script>
</body>
</html>
/* styles.css */
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f4f4f9;
  margin: 0;
}

.container {
  width: 80%;
  max-width: 600px;
  text-align: center;
}

textarea {
  width: 100%;
  height: 100px;
  margin: 10px 0;
  padding: 10px;
  font-size: 16px;
}

.buttons {
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

#result {
  margin-top: 20px;
  font-size: 18px;
}
// app.js

async function useOpenAI() {
  const input = document.getElementById("userInput").value;
  const resultElement = document.getElementById("result");

  try {
    const response = await fetch("https://api.openai.com/v1/engines/davinci/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer YOUR_OPENAI_API_KEY`
      },
      body: JSON.stringify({
        prompt: input,
        max_tokens: 100
      })
    });
    const data = await response.json();
    resultElement.innerText = data.choices[0].text;
  } catch (error) {
    console.error("Error with OpenAI API:", error);
    resultElement.innerText = "Error connecting to OpenAI";
  }
}

async function useHuggingFace() {
  const input = document.getElementById("userInput").value;
  const resultElement = document.getElementById("result");

  try {
    const response = await fetch("https://api-inference.huggingface.co/models/gpt2", {
      method: "POST",
      headers: {
        "Authorization": `Bearer YOUR_HUGGING_FACE_API_KEY`
      },
      body: JSON.stringify({ inputs: input })
    });
    const data = await response.json();
    resultElement.innerText = data[0].generated_text;
  } catch (error) {
    console.error("Error with Hugging Face API:", error);
    resultElement.innerText = "Error connecting to Hugging Face";
  }
}

async function useCustomAI() {
  const input = document.getElementById("userInput").value;
  const resultElement = document.getElementById("result");

  // Example of another AI tool integration (e.g., another API or local model)
  try {
    const response = await fetch("https://example.com/your-ai-api", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer YOUR_CUSTOM_AI_API_KEY`
      },
      body: JSON.stringify({ text: input })
    });
    const data = await response.json();
    resultElement.innerText = data.result;
  } catch (error) {
    console.error("Error with Custom AI API:", error);
    resultElement.innerText = "Error connecting to Custom AI";
  }
}
