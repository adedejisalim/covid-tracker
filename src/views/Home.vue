<template>
  <div class="home">
    Hello world
  </div>
</template>

<script>


export default {
  name: 'Home',
  components: {
    
  },
  //Create placeholders to store the data from the API
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    //Create method to get the covid data I need from the API
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data
    }
  },

  //Runs as soon as the site is loaded
  async created(){
    const data = await this.fetchCovidData()
  
    this.dataDate = data.date
    this.stats = data.global
    this.countries = data.countries
    this.loadingImage = false
  }
}
</script>
