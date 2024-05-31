"# WeatherApp" 
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        * html, body{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    
    font-family: 'montserrat', sans-serif;
    background-image: url(backgrd.jpg);
    background-size: cover;
    background-position: top center;
}

.app-wrap {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.1), rgba(0,0,0,0.1));
}

header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 50px 15px 15px;
}

header input {
    width: 100%;
    max-width: 280px;
    margin-top: 25px;
    padding: 10px;
    border: none;
    outline: none;
    background-color: rgba(0,0,0,0.6);
    border-radius: 16px 16px 0px 16px;
    border-right: 3px solid rgba(0,0,0,0.8);
    border-bottom: 3px solid rgba(0,0,0,0.8);
    color: whitesmoke;
    font-size: 20px;
    font-weight: 300;
    transition: 0.2s ease-out;
}

header input:focus{
    background-color: rgba(0,0,0,0.5);
}

main {
    flex: 1 1 100%;
    padding: 25px 25px 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.location .city {
    font-size: 70px;
    font-weight: 600;
    margin-bottom: 10px;
    font-family: 'Times New Roman';
    color: black;
}

.location .date {
    font-size: 30px;
    font-weight: bold;
    font-family: 'Times New Roman', Times, serif;
    font-style: oblique;
    color: black;
}

.current .temp {
    font-family: 'Times New Roman';
    font-size: 120px;
    font-weight: 900;
    margin: 20px;
    text-shadow: 2px 10px rgba(255,255,255,0.5);
    color: black;
}

.current .temp span {
    font-weight: 500;
}

.current .weather {
    color: black;
    font-size: 40px;
    font-weight: 900;
    font-family: 'Times New Roman';
    margin-bottom: 15px;
}

.current .hi-low {
    color: black;
    font-size: 25px;
    font-family: 'Times New Roman';
    font-style: oblique;
    font-weight: 800;
}
    </style>
</head>

<body>
    <div class="app-wrap">
        <header>
            <input type="text" autocomplete="off" class="search-box" placeholder="Konumunuzu Girin......" />
        </header>
        <main>
            <section class="location">
                <div class="city">ISTANBUL, TR</div>
                <div class="date">Tuesday 7 May 2024</div>
            </section>
            <div class="current">
                <div class="temp">25<span>°C</span></div>
                <div class="weather">Clear</div>
                <div class="hi-low">20°C</div>
            </div>
        </main>
    </div>
    <script>
        const api = {
    key: "6186c89f2fffc2195b93eb0338c72f51",
    base: "https://api.openweathermap.org/data/2.5/"
}
  
const searchbox = document.querySelector('.search-box');
searchbox.addEventListener('keypress', setQuery);
  
function setQuery(evt) {
    if (evt.keyCode == 13) {
      getResults(searchbox.value);
    }
}
  
function getResults (query) {
    fetch(`${api.base}weather?q=${query}&units=metric&APPID=${api.key}`)
      .then(weather => {
        return weather.json();
      }).then(displayResults);
}
  
function displayResults (weather) {
    let city = document.querySelector('.location .city');
    city.innerText = `${weather.name}, ${weather.sys.country}`;
  
    let now = new Date();
    let date = document.querySelector('.location .date');
    date.innerText = dateBuilder(now);
  
    let temp = document.querySelector('.current .temp');
    temp.innerHTML = `${Math.round(weather.main.temp)}<span>°C</span>`;
  
    let weather_el = document.querySelector('.current .weather');
    weather_el.innerText = weather.weather[0].main;
  
    let hilow = document.querySelector('.hi-low');
    hilow.innerText = `${Math.round(weather.main.temp_min)}°C / ${Math.round(weather.main.temp_max)}°C`;
}
  
function dateBuilder (d) {
    let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
    let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
  
    let day = days[d.getDay()];
    let date = d.getDate();
    let month = months[d.getMonth()];
    let year = d.getFullYear();
  
    return `${day} ${date} ${month} ${year}`;
}
    </script>
</body>

</html>
