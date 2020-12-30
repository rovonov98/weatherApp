<template>
    <div class="weather-app" :class=" ifDay ? 'isDay' : 'isNight'">
        <div class="weather-wrapper">
            <div class="weather-input">
                <h3 class="h3">Weather in</h3>
                <form
                class="input-form"
                @submit.prevent="getWeather">
                    <input
                    class="input" 
                    type="text" 
                    v-model="citySearch"
                    placeholder="City">
                </form>
            </div>
            <div class="weather-output" v-if="isSearched">
                <div class="output-inner">
                    <div class="top-output">
                        <p class="output-city">{{ weather.city }}</p>
                        <div class="output-dots">
                            <div class="dot"></div>
                            <div class="dot"></div>
                            <div class="dot"></div>
                        </div>
                        <p class="output-country">{{ weather.country }}</p>
                    </div>
                    <div class="bottom-output">
                        <span class="output-temperature">{{ weather.temperature }}&deg;C</span>
                        <p class="output-description">{{ weather.description }}</p>
                        <div class="top_bot-temperatures">
                            <span class="output-top-bot">{{ weather.bottomTemp }}&deg;C</span>
                            <span class="output-top-bot">{{ weather.topTemp }}&deg;C</span>
                        </div>
                        <div class="FL-humidity">
                            <div class="output-wrapper">
                                <span class="output-FL">{{ weather.feelsLike }}&deg;C</span>
                                <p class="wrapper-description">Feels like</p>
                            </div>
                            <div class="output-wrapper">
                                <span class="output-humidity">{{ weather.humidity }}%</span>
                                <p class="wrapper-description">Humidity</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Weather',
    data() {
        return {
            ifDay: true,
            citySearch: '',
            isSearched: false,
            weather: {
                country: '',
                city: '',
                temperature: 0,
                description: '',
                topTemp: 0,
                bottomTemp: 0,
                feelsLike: 0,
                humidity: 0,
            }
        }
    },
    methods: {
        getWeather: async function() {
            console.log(this.citySearch)
            const key = '5299e83c9cf2fef510fb8ddaa3206ac8'
            const baseURL = `https://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&appid=${key}&units=metric`
            const response = await fetch(baseURL)
            const data = await response.json()
            console.log(data)
            this.citySearch = ''
            this.weather.city = data.name
            this.weather.country = data.sys.country
            this.weather.temperature = Math.round(data.main.temp)
            this.weather.description = data.weather[0].description
            this.weather.topTemp = Math.round(data.main.temp_max)
            this.weather.bottomTemp = Math.round(data.main.temp_min)
            this.weather.feelsLike = Math.round(data.main.feels_like)
            this.weather.humidity = Math.round(data.main.humidity)
            //time
            const time = data.weather[0].icon
            if (time.includes("n")) {
                this.ifDay = false
            } else {
                this.ifDay = true
            }
            this.isSearched = true  
        }
    }
}
</script>

<style lang="scss">
.isDay {
    background: $second-gradient;
}
.isNight {
    background: $third-gradient;
    color: $second-color
}
.weather-app {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    height: 100vh;
    margin: 0 auto;
    font-size: 1.5rem;
    font-family: sans-serif;
}
.weather-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    @media(max-width: 576px) {
        width: 85%;
    }
    @media(min-width: 576px) {
        width: 75%;
    }
    @media(min-width: 768px) {
        width: 65%;
    }
    @media(min-width: 992px) {
        width: 50%;
    }
    @media(min-width: 1200px) {
        width: 30%;
    }
}
.weather-input {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
}
.input-form {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 1rem;
    border: none;
    width: 100%;
}
.input {
    width: 100%;
    padding: 1em;
    border-radius: 30px;
    border: 1px solid $first-color;
    &:focus {
        border-radius: 30px;
        border: 1px solid $third-color;
        outline: none;
    }
}
.weather-output {
    display: flex;
    justify-content: center;
    align-items: center;
    background: $first-gradient;
    padding: 2rem;
    color: $second-color;
    border-radius: 30px;
    width: 100%;
}
.output-inner {
    width: 80%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.top-output {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.output-city {
    font-size: 2rem;
    margin: 1rem;
}
.output-dots {
    display: flex;
    justify-content: center;
    align-items: center;
    
}
.dot {
    background: $second-color;
    width: 5px;
    height: 5px;
    margin: 5px;
    border-radius: 50%;

}
.output-country {
    margin: 2em;
}

.bottom-output {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.output-temperature {
    font-size: 3rem;
}
.output-description {
    font-size: 1.5rem;
    margin: 1rem;
}
.top_bot-temperatures {
    margin: 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
}
.output-top-bot {
    padding: 1rem;
}
.FL-humidity {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
}
.output-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 1rem;
}
.wrapper-description {
    font-size: 1rem;
}

</style>
