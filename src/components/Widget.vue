<template>
  <q-card class="q-pa-md" bordered>
    <div class="text-center">
      <h3>Weather Widget</h3>
      <q-input
        outlined
        dense
        v-model="city"
        label="Masukkan nama kota"
        @keyup.enter="searchWeather"
      />
      <q-btn @click="searchWeather" label="Cari" class="q-mt-md" />
      <div v-if="!isLoading && weatherData">
        <div class="Out">
          <p>{{ cityName }} {{ weatherData.main.temp.toFixed(0) }}°</p>
          <p>{{ getWeatherDescription(weatherData.weather[0].description) }}</p>
        </div>
      </div>
      <div v-else-if="!isLoading && !weatherData" class="Output">
        <p>Masukkan nama kota dan tekan Cari</p>
      </div>
      <div v-if="isLoading">
        <q-spinner-hourglass size="40px" color="primary" />
      </div>
    </div>
  </q-card>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      cityName: '',
      weatherData: null,
      isLoading: false
    };
  },
  methods: {
    searchWeather() {
      if (this.city.trim() === '') {
        alert('Masukkan nama kota terlebih dahulu');
        return;
      }
      
      this.isLoading = true;
      this.cityName = this.city; 
      
      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=706de072a287f99fe56182b6caa08be1&units=metric`)
        .then(response => response.json())
        .then(data => {
          this.weatherData = data;
        })
        .catch(error => {
          console.error('Error fetching weather data:', error);
          alert('Terjadi kesalahan saat mengambil data cuaca');
        })
        .finally(() => {
          this.isLoading = false; 
          this.city = ''; 
        });
    },
    getWeatherDescription(description) {
      const weatherMap = {
        'clear sky': 'Langit Cerah',
        'few clouds': 'Berawan Sedikit',
        'scattered clouds': 'Berawan',
        'overcast clouds': 'Berawan Mendung',
        'shower rain': 'Hujan Gerimis',
        'rain': 'Hujan',
        'moderate rain' :'Hujan Sedang',
        'thunderstorm': 'Hujan Petir',
        'snow': 'Salju',
        'mist': 'Kabut',
        'smoke': 'Asap',
        'haze': 'Kabut Asap',
        'fog': 'Kabut Tebal',
        'sand': 'Angin Pasir',
        'dust': 'Debu',
        'ash': 'Abu Vulkanik',
        'squall': 'Angin Kencang',
        'tornado': 'Tornado'
      };

      return weatherMap[description] || description;
    }
  }
};
</script>

<style>
.Out{
  margin-top: 30px;
  border: 1px solid black;
  padding: 50px;
}
.Output{
  margin-top: 10px;
}
</style>