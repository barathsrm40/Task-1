# Task-1
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Weather App - API Integration</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 20px;
      text-align: center;
    }
    .weather-container {
      background-color: #fff;
      border-radius: 10px;
      padding: 30px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      max-width: 400px;
      margin: auto;
    }
    input {
      padding: 10px;
      margin-top: 10px;
      width: 80%;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      margin-top: 10px;
      background: #007BFF;
      color: white;
      border: none;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="weather-container">
    <h2>Weather Checker 🌤️</h2>
    <input type="text" id="cityInput" placeholder="Enter city name"/>
    <button onclick="getWeather()">Check Weather</button>
    <div class="result" id="weatherResult"></div>
  </div>

  <script>
    async function getWeather() {
      const city = document.getElementById("cityInput").value;
      const apiKey = "YOUR_API_KEY"; // Replace with your OpenWeatherMap API key
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const response = await fetch(url);
        if (!response.ok) throw new Error("City not found");

        const data = await response.json();
        document.getElementById("weatherResult").innerHTML = `
          <h3>${data.name}, ${data.sys.country}</h3>
          <p><strong>Temperature:</strong> ${data.main.temp}°C</p>
          <p><strong>Weather:</strong> ${data.weather[0].description}</p>
          <p><strong>Humidity:</strong> ${data.main.humidity}%</p>
          <p><strong>Wind Speed:</strong> ${data.wind.speed} m/s</p>
        `;
      } catch (error) {
        document.getElementById("weatherResult").innerHTML = `<p style="color:red;">${error.message}</p>`;
      }
    }
  </script>
</body>
</html>
