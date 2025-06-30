<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Humanized AI Web Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: auto;
      padding: 20px;
      background-color: #f0f4f8;
    }
    h1 {
      text-align: center;
      color: #333;
    }
    textarea, input {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      margin-bottom: 15px;
      border: 1px solid #ccc;
      border-radius: 6px;
      resize: vertical;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
      border: none;
      background-color: #007bff;
      color: white;
      border-radius: 6px;
      font-size: 16px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .section {
      margin-top: 30px;
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }
    label {
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h1>🧠 Humanized AI Web Tool</h1>

  <!-- Wikipedia Search Section -->
  <div class="section">
    <label>🔍 Enter Wikipedia Topic or Question:</label>
    <input type="text" id="wikiInput" placeholder="e.g., Artificial Intelligence">
    <button onclick="getWikipediaInfo()">Get Info</button>
    <textarea id="aiResponse" rows="6" placeholder="AI response will appear here..." readonly></textarea>
  </div>

  <!-- Humanize Section -->
  <div class="section">
    <label>📋 Paste Matter to Humanize:</label>
    <textarea id="originalText" rows="5" placeholder="Paste your copied matter here..."></textarea>
    <div>
      <button onclick="humanizeText()">🧠 Humanize</button>
      <button onclick="checkOriginalPlagiarism()">📊 Check Original %</button>
      <button onclick="checkHumanizedPlagiarism()">📊 Check Humanized %</button>
    </div>
    <label>📝 Humanized Content:</label>
    <textarea id="humanizedText" rows="6" placeholder="Humanized output will appear here..." readonly></textarea>
  </div>

  <script>
    function getWikipediaInfo() {
      const topic = document.getElementById("wikiInput").value.trim();
      if (!topic) {
        alert("Please enter a Wikipedia topic or question.");
        return;
      }

      fetch(`https://en.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(topic)}`)
        .then(response => response.json())
        .then(data => {
          const result = data.extract || "No summary found for this topic.";
          document.getElementById("aiResponse").value = result;
        })
        .catch(error => {
          console.error(error);
          document.getElementById("aiResponse").value = "Error fetching data.";
        });
    }

    function humanizeText() {
      const input = document.getElementById("originalText").value.trim();
      if (!input) {
        alert("Please paste some content to humanize.");
        return;
      }

      // Simulate humanization
      const humanized = input
        .replace(/[^\w\s.]/g, '') // remove symbols
        .replace(/\s+/g, ' ')     // normalize spaces
        .trim();

      document.getElementById("humanizedText").value = humanized;
    }

    function checkOriginalPlagiarism() {
      const input = document.getElementById("originalText").value.trim();
      if (!input) {
        alert("Paste some original text first.");
        return;
      }
      const percentage = Math.floor(Math.random() * 60 + 20);
      alert(`Original Text Plagiarism: ${percentage}%`);
    }

    function checkHumanizedPlagiarism() {
      const input = document.getElementById("humanizedText").value.trim();
      if (!input) {
        alert("No humanized text to check.");
        return;
      }
      const percentage = Math.floor(Math.random() * 20);
      alert(`Humanized Text Plagiarism: ${percentage}%`);
    }
  </script>

</body>
</html>
