<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info">Breweries List</h1>
        <h2></h2>
      </div>
      <!-- /.col-12 -->
    </div>
    <!-- /.row -->
    <div class="row">
      <div class="col-6 ">
        <BrewList @mouse-over-brew="mouseOverBrew" @mouse-left-brew="mouseLeftBrew" :brews="brews"/>
      </div>
      <!-- /.col-6 -->
      <div class="col-6">

          <BrewMap :brews="brews"/>

      </div>
      <!-- /.col-6 -->
    </div>
    <!-- /.row -->
  </div>
  <!-- /.container -->
</template>

<script>
import axios from 'axios'
import BrewList from './BrewList.vue'
import BrewMap from './BrewMap.vue'

export default {
  name: 'Brew',
  components:{
    BrewList,
    BrewMap
  },
  data(){
    return{
      brews:[],
      normalIcon:[15,15],
      largeIcon:[50,50]
    }
  },
  methods:{
    mouseOverBrew(index){
      this.brews[index].iconSize = this.largeIcon;
    },
    mouseLeftBrew(index){
      this.brews[index].iconSize = this.normalIcon;
    }
  },
  mounted(){
    axios.get('https://api.openbrewerydb.org/breweries/')
    .then(response =>
    this.brews = response.data.filter(item => item.state === "Arizona").map(r=>{r.iconSize = this.normalIcon;
    return r;}))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

</style>
