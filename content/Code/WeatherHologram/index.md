---
title: "Weather Hologram"
draft: false
date: 2025-07-27
description: "Weather Hologram"
tags: ["weather", "hologram"]
showHero: false
---
<style>
    html, body {
      margin: 0;
      padding: 0;
      background: black;
      width: 100%;
      min-height: 100vh;
      overflow-y: auto;
      font-family: 'Roboto', sans-serif;
    }

    /* Wrap everything to mirror */
    #mirrorWrapper {
      -webkit-transform: scaleX(-1);
      -moz-transform: scaleX(-1);
      -ms-transform: scaleX(-1);
      -o-transform: scaleX(-1);
      transform: scaleX(-1);
    }

    #container {
      text-align: center;
      padding-top: 20px;
    }

    #weatherImg {
      transform: scale(1.5);
      transform-origin: center;
      max-width: 100%;
      height: auto;
    }

    #spacer {
      height: 150px;
    }

    #tempDisplay {
      position: absolute;
      top: 20px;
      right: 20px;
      color: white;
      font-size: 40px;
      font-weight: 100;
      z-index: 999;
      pointer-events: none;
    }
  </style>

<div id="mirrorWrapper">
  <div id="tempDisplay">--°C</div>
  <div id="container">
    <img id="weatherImg" src="sun.gif" alt="Ambient Weather Display">
  </div>
  <div id="spacer"></div>
</div>

<script>
  var gifs = {
    "Clear": "sun.gif",
    "Clouds": "clouds.gif",
    "Rain": "rain.gif",
    "Drizzle": "rain.gif",
    "Mist": "haze.gif",
    "Smoke": "haze.gif",
    "Haze": "haze.gif",
    "Fog": "haze.gif",
    "Thunderstorm": "thunderstorm.gif",
    "Default": "sun.gif"
  };

  var apiKey = "0279ec960d72c1817406752c091587fd";
/*    var apiKey = "0b6dae9987379e1deaf001865ec26a64"; */
  var lat = "43.30";
  var lon = "-77.92";
  var apiUrl = "https://api.openweathermap.org/data/2.5/weather?lat=" + lat + "&lon=" + lon + "&units=imperial&appid=" + apiKey;

  function updateImage(condition) {
    var gifSrc = gifs[condition] || gifs["Default"];
    document.getElementById("weatherImg").src = gifSrc;
  }

  function updateTempDisplay(temp) {
    var display = document.getElementById("tempDisplay");
    display.textContent = Math.round(temp) + "°F";
  }

  function fetchWeather() {
    var xhr = new XMLHttpRequest();
    xhr.open("GET", apiUrl, true);
    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
        try {
          var data = JSON.parse(xhr.responseText);
          if (data && data.weather && data.weather.length > 0) {
            var condition = data.weather[0].main;
            var temp = data.main.temp;
            updateImage(condition);
            updateTempDisplay(temp);
          }
        } catch (e) {
          console.error("Error parsing JSON response:", e);
        }
      }
    };
    xhr.send();
  }

  fetchWeather();
  setInterval(fetchWeather, 600000);
</script>


<div style="text-align: center;">
  <div style="width: 500px; margin: 0 auto; background: #000; color: #fff;">Inspiration and code from <a href="https://www.instructables.com/Trap-the-Current-Weather-in-a-Box/">here</a>. Pics of the project coming soon!</div>

</div> 
