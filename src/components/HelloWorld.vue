

<template>
  <div v-if="onReady">
    <label for="city">City:</label>
    <select id="city" v-model="cityName">
      <!-- <option value="">city...</option> -->
      <option v-for="(c, index) in cities" :value="index">
        {{c.city}}
      </option>
    </select>
    <label for="area">Area:</label>
    <select id="area" v-if="areas" v-model="areaName">
      <option value="">--</option>
      <option v-for="(a,index) in areas" :value="index">
        {{a.text}}
      </option>
    </select>
    <label for="zip">Zip:</label>
    <span id="zip" v-if="areaCode">{{areaCode}}</span>
    <span v-else>--</span>
  </div>
  <div v-else>
    loading...
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data(){
    return {
      onReady : false,
      cities : [],
      cityName: '',
      areas : [],
      areaName:'',
      areaCode: ''
    }
  },
  props:['idx'],
  methods: {
  },
  watch: {
    cities(index){
      // console.log('cities is changed')
      this.cityName = 0
    },
    cityName(index){
      // console.log('cityname is changed')
      this.areas = this.cities[index].area
      this.areaName = 0
      this.areaCode = this.areas[0].zip
      // console.log(this.areas)
    },
    areaName(index){
      // console.log('areaName is changed')
      this.areaCode = this.areas[index].zip
    }
  },
  mounted() {
    axios
      .get('data/bins/1cyheo')
      .then((res) => {
          this.cities = res.data.taiwan
          // this.cityName = this.cities[0].city
          // this.areaName = this.cities[0].area
          // console.log(this.cityName);
          
          this.onReady = true
          // console.log(res.data.taiwan)
      }
    )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
