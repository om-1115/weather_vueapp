<template>
<div id="weather" :class="istem? 'cold' : 'warm' ">
    <main>
        <div class="search-box">
            <input type="text" class="search-bar" placeholder="Search the city.." v-model="citysearch" @keyup.enter="fetchweather()" />
        </div>
        <div class="weather-wrap">
            <div class="location-box">
                <div class="location">{{city}} {{country}}</div>
                <div class="date">{{dateBuilder()}}</div>
            </div>
            <div class="weather-box">
                <div class="temperature">{{Math.round(temperatuea)}}°C</div>

                <div class="weather-season">{{weath}}</div>
            </div>
        </div>
    </main>
</div>
</template>

<script>
// import axios from 'axios'

export default {
    name: 'App',
    data() {
        return {
            istem:'true',
            citysearch: "",
            city: "",
            temperatuea: "",
            weath: "",
            country: "",
        }
    },
    methods: {
        async fetchweather() {

            console.log(this.citysearch);
            // const key = "66fa1fe7b11bee5fa41862cb6af2cd34";
            const baseURL = `https://api.openweathermap.org/data/2.5/weather?q=${this.citysearch}&appid=66fa1fe7b11bee5fa41862cb6af2cd34&units=metric`;
            const response = await fetch(baseURL)

            const datax = await response.json();
            console.log(datax);
            this.citysearch = "";
            this.city = datax.name;
            this.temperatuea = datax.main.temp;
            this.weath = datax.weather[0].main;
            this.country = datax.sys.country;

            if(this.temperatuea>'16')
            {
              this.istem='false'
            }
            else{
              this.istem='true'
            }
        },
        dateBuilder() {
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return `${day} ${date} ${month} ${year}`;
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@500;700&display=swap');

* {
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;

}

body {
    font-family: 'Poppins', sans-serif;
 
}

#weather {
     
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
} 

.warm {
    background-image: url('./assets/wallpaperflare.com_wallpaper\ \(5\).jpg');
    
}
.cold{
  background-image: url('./assets/wallpaperflare.com_wallpaper\ \(4\).jpg');
  
}

main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.15), rgba(0, 0, 0, 0.75));
}

.search-box {
    width: 100%;
    margin-bottom: 30px;
}

.search-box .search-bar {
    display: block;
    width: 50%;
    margin: auto;
    margin-bottom: 48px;

    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    outline: none;
    border: none;
    background: none;
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.55);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s
}

.search-box .search-bar:focus {
    background-color: rgba(255, 255, 255, 0.5);
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.55);
    border-radius: 16px 0px 16px 0px;
}

.location-box .location {
    color: white;
    font-size: 40px;
    font-weight: bolder;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
    color: white;
    font-size: 20px;
    font-weight: lighter;
    /* font-style: italic; */
    text-align: center;
    /* margin-top: 5px; */
}

.weather-box {
    text-align: center;
}

.weather-box .temperature {
    display: inline-block;
    padding: 10px 25px;
    color: white;
    font-size: 102px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.15);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 16px;
    margin: 30px 0px;
    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather-season {
    color: white;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
