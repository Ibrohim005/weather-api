<template>
  <div
    class="main w-full h-screen text-center flex items-center content-center"
  >
    <div class="lg:container mx-auto px-60">
      <div
        class="flex flex-col-reverse lg:flex-row items-center justify-between"
      >
        <div class="main-info p-3 lg:p-5 rounded-xl">
          <h3 class="main__title">
            {{ weather.name }}, {{ weather.sys.country }}
          </h3>
          <p class="main__date">
            {{ dateBuilder }}
          </p>
          <h1 class="main__temp">{{ Math.round(weather.main.temp) }}°C</h1>
        </div>
        <div>
          <input
            v-model="query"
            class="
              main__input
              mb-4
              lg:mb-0
              p-4
              transition
              rounded-xl
              border border-transparent
              focus:outline-none
              focus:ring-2
              focus:ring-red-600
              focus:border-transparent
            "
            type="text"
            placeholder="Enter your country!"
            @keypress.enter="fetchWeather"
          />
        </div>
      </div>
    </div>
    <img
      src="../assets/bg.jpg"
      alt=""
      class="bg w-full h-full fixed top-0 left-0"
      style="z-index: -1"
      git
    />
  </div>
</template>

<script>
export default {
  name: "Home",
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
  &-info {
    background-color: rgba(255, 255, 255, 0.6);
  }
  &__temp {
    font-size: 80px;
  }
}
</style>
