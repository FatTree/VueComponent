<template>
    <div id="app2">
        <h1>CITY SELECTOR OF TAIWAN!((app2))</h1>
        <div v-if="onReady">
            <citySelector v-model="cityIndex" :data-source="allCities" :dataName="city" :oIndex="cityIndex" @input="changed"></citySelector>
            <citySelector v-model="areaIndex" :data-source="allAreas" :dataName="area" :oIndex="areaIndex" @input2="changed2"></citySelector>
            <label>Zip:{{ zip }}</label>
        </div>
        <div v-else>
            temp2 is loading...
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import citySelector from './components/citySelector'
export default {
    name: 'App2',
    data(){
        return {
            onReady : false,
            allCities : [],
            allAreas : [],
            zip: '',
            cityIndex: 0,
            areaIndex: 0,
            city: 'city',
            area:'text'
        }
    },
    methods:{
        changed(val){
            this.allAreas = this.allCities[val].area
            this.areaIndex = 0
            this.zip = this.allAreas[this.areaIndex].zip
        },
        changed2(val){
            this.zip = this.allAreas[val].zip
        }
    },
    mounted(){
        axios
            .get('data/bins/1cyheo')
            .then((res) => {
                this.allCities = res.data.taiwan
                this.allAreas = this.allCities[this.cityIndex].area
                this.zip = this.allAreas[this.areaIndex].zip
                this.onReady = true
            })
    },
    components: { citySelector }
}
</script>

<style>
#app2 {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>