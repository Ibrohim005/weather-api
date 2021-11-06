<template>
  <router-view />
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "9eb96ce8f399f176e4c79b19ba9cc023",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {
        name: "Tashkent",
        sys: {
          country: "Uz",
        },
        main: {
          temp: "16",
        },
      },
    };
  },
  computed: {
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} | ${date} | ${month} | ${year}`;
    },
  },
  methods: {
    fetchWeather() {
      fetch(
        `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.weather = results;
    },
  },
};
</script>

<style lang="scss">
.main {
  background: url("./assets/bg.jpg") no-repeat;
  background-size: cover;
  width: 100%;
  height: 100vh;
  &-info {
    background-color: rgba(255, 255, 255, 0.6);
    border-radius: 10px;
  }
  &__temp {
    font-size: 80px;
  }
}
</style>
