<template>
  <v-container grid-list-xs>
    <!-- <v-layout> -->
    <h1 class="display-1 text-center pb-5">
      Weather App
    </h1>
    <v-flex xs12>
      <v-card color="blue-grey darken-2" dark>
        <v-card-text>
          <v-layout class="text-center">
            <v-flex v-if="weather.weather" xs4 class="text-xs-center">
              <h4>Temperature</h4>
              <h1 class="display-1" v-html="weather.name" />
              <img :src="icon" alt="weather icon">
              <p>
                <span class="display-1">{{ temp() }} &deg;C</span>
                <span class="caption ml-4">
                  {{ weather.weather[0].description }}
                </span>
              </p>
            </v-flex>
            <v-flex v-if="weather.weather" xs4 class="text-xs-center">
              <h4>Wind & Pressure</h4>
              <h3 class="headline mt-4">
                Wind: {{ weather.wind.speed }} m/s ({{ weather.wind.deg }} &deg;)
              </h3>
              <h3 class="headline mt-4">
                Humidity: {{ weather.main.humidity }}%
              </h3>
              <h3 class="headline mt-4">
                Pressure: {{ weather.main.pressure }} hPa
              </h3>
            </v-flex>
            <v-flex v-if="weather.weather" xs4 class="text-xs-center">
              <h4>Other:</h4>
              <h3 class="headline mt-4">
                Max Temperature: {{ max_temp }} &deg; C
              </h3>
              <h3 class="headline mt-4">
                Min Temperature: {{ min_temp }} &deg; C
              </h3>
            </v-flex>
          </v-layout>
        </v-card-text>
      </v-card>
    </v-flex>

    <v-flex class="mt-4">
      <v-form @submit.prevent="getWeatherInfo">
        <v-text-field
          v-model="city"
          counter="25"
          hint="This field uses counter prop"
          label="Enter City Name"
          solo
        />
      </v-form>
    </v-flex>
    <!-- </v-layout> -->
  </v-container>
</template>

<script>
export default {
  asyncData ({ params, $axios }) {
    return $axios
      .$get('https://api.openweathermap.org/data/2.5/weather?q=London&appid=c8c7931730800b1584836813834bd2b2')
      .then((res) => {
        return {
          weather: res
        }
      })
  },

  data () {
    return {
      city: '',
      api_key: 'c8c7931730800b1584836813834bd2b2'
    }
  },

  computed: {
    max_temp () {
      return Math.round(this.weather.main.temp_max - 273)
    },
    min_temp () {
      return Math.round(this.weather.main.temp_min - 273)
    },
    icon () {
      return this.weather.weather
        ? `http://openweathermap.org/img/wn/${this.weather.weather[0].icon}@2x.png`
        : ''
    }
  },

  methods: {
    getWeatherInfo () {
      this.$axios
        .$get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.api_key}`
        )
        .then((res) => {
          this.weather = res
        })
    },

    temp () {
      return this.weather.main ? Math.round(this.weather.main.temp - 273) : ''
    }
  }
}
</script>
