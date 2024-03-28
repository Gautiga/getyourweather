<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="./public/styles/main.css">
    
</head>
<body>
    <div class="card">
        <h1 class="heading">Get Your City's Weather</h1>
        <div class="search">
            <input type="text" placeholder="enter your city name"
            spellcheck="false">
            <button ><svg class =  "abcd http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path d="M416 208c0 45.9-14.9 88.3-40 122.7L502.6 457.4c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L330.7 376c-34.4 25.2-76.8 40-122.7 40C93.1 416 0 322.9 0 208S93.1 0 208 0S416 93.1 416 208zM208 352a144 144 0 1 0 0-288 144 144 0 1 0 0 288z"/></svg></button>
        </div>
        <div class="error">
            <p>Invalid city Name</p>
        </div>
        <!-- <div class="more">
            <div class="date">Date:</div>
            <div class="time">time:</div>

        </div> -->
        <div class="weather">
            <img src="./public/images/rain.png" class="weather-icon">
            <h1 class="temp">__°C</h1>
            <h2 class="city">__</h2>
            <div class="details">
            <div class="col">
                <img src="./public/images/humidity.png">
                <div>
                    <p class="humidity">..</p>
                    <p>Humidity</p>
                </div>
            </div>
            <div class="col">
                <img src="./public/images/wind.png">
                <div>
                    <p class="Wind">.. kmph</p>
                    <p>Wind Speed</p>
                </div>
            </div>
        </div>
        </div>
    </div>

    <script >
       const apiKey = "5afd2151348e504c331841b5610d900f";
const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";
const searchBox = document.querySelector(".search input");
const searchBttn = document.querySelector(".search button");
const weatherImg = document.querySelector(".weather-icon");

// const dateToday = new Date();

// creating function for weather data

async function checkWeather(city){
    const response = await fetch(apiUrl + city + `&appid=${apiKey}`);

if (response.status == 404){
    document.querySelector(".error").style.display = "block";
    document.querySelector(".weather").style.display = "none";
} else {
    var data = await response.json();
    
    // changinng city, temp, humidity $ wind speed as per weather data
    document.querySelector(".city").innerHTML = data.name;
    document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°C";
    document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
    document.querySelector(".Wind").innerHTML = data.wind.speed + " kmph";
    
    // document.querySelector(".date").innerHTML = new Date();

// changing the photo according to thr weather

    if(data.weather[0].main == "Clouds"){
weatherImg.src = "./public/images/clouds.png";
    } 
    else if (data.weather[0].main == "Clear"){
        weatherImg.src = "./public/images/clear.png" 
    } else if (data.weather[0].main == "Drizzle"){
        weatherImg.src = "./public/images/drizzle.png"
    } else if (data.weather[0].main == "Rain"){
        weatherImg.src = "./public/images/rain.png"
    } else if (data.weather[0].main == "Snow"){
        weatherImg.src = "./public/images/snow.png"
    } else if (data.weather[0].main == "Mist"){
        weatherImg.src = "./public/images/mist.png"
    }
    document.querySelector(".weather").style.display = "block";
    document.querySelector(".error").style.display = "none";
}


}
searchBttn.addEventListener("click", ()=>{
    checkWeather(searchBox.value);
})
    

checkWeather();
    </script>

</body>
</html>
