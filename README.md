index.html:

<html>
<head>
  <title>Temperature Converter</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>🌡️ Temperature Converter</h1>
    <div class="card">
      <input type="number" id="tempInput" placeholder="Enter temperature" />
      <select id="unitSelect">
        <option value="celsius">Celsius</option>
        <option value="fahrenheit">Fahrenheit</option>
        <option value="kelvin">Kelvin</option>
      </select>
      <button onclick="convertTemp()">Convert</button>
      <div id="result" class="fade"></div>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>


style.css:

@keyframes animatedGradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(-45deg, #f3ec78, #af4261, #23a6d5, #23d5ab);
  background-size: 400% 400%;
  animation: animatedGradient 15s ease infinite;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  text-align: center;
  color: #fff;
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 30px;
  text-shadow: 2px 2px 6px #000;
}

.card {
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 30px;
  width: 350px;
  backdrop-filter: blur(10px);
  box-shadow: 0 8px 16px rgba(0,0,0,0.3);
}

input, select, button {
  display: block;
  width: 100%;
  margin: 15px 0;
  padding: 12px;
  font-size: 16px;
  border-radius: 10px;
  border: none;
  outline: none;
}

input, select {
  background: #ffffffcc;
  color: #333;
}

button {
  background: linear-gradient(to right, #ff416c, #ff4b2b);
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:hover {
  background: linear-gradient(to right, #ff4b2b, #ff416c);
  transform: scale(1.05);
}

#result {
  margin-top: 20px;
  font-size: 22px;
  font-weight: bold;
  color: #fff;
  transition: opacity 0.5s ease-in;
  opacity: 0;
}

#result.show {
  opacity: 1;
}


script.js:

function convertTemp() {
  const input = document.getElementById("tempInput").value;
  const unit = document.getElementById("unitSelect").value;
  const resultDiv = document.getElementById("result");

  if (isNaN(input) || input === "") {
    resultDiv.innerHTML = "❌ Please enter a valid number.";
    resultDiv.classList.add("show");
    return;
  }
  let temp = parseFloat(input);
  let result = "";
  if (unit === "celsius") {
    result = `Fahrenheit: ${(temp * 9/5 + 32).toFixed(2)} °F<br>Kelvin: ${(temp + 273.15).toFixed(2)} K`;
  } else if (unit === "fahrenheit") {
    result = `Celsius: ${((temp - 32) * 5/9).toFixed(2)} °C<br>Kelvin: ${(((temp - 32) * 5/9) + 273.15).toFixed(2)} K`;
  } else if (unit === "kelvin") {
    result = `Celsius: ${(temp - 273.15).toFixed(2)} °C<br>Fahrenheit: ${((temp - 273.15) * 9/5 + 32).toFixed(2)} °F`;
  }
  resultDiv.innerHTML = `✅ Converted Temperature:<br>${result}`;
  resultDiv.classList.add("show");
}
