<template>
  <div class="card brew-list">
	<ul class="list-group list-group-flush">
	<li class="list-group-item" v-for="(brew,index) in brews" :key="index">{{index}} - {{brew.name}} - {{brew.state}}</li>
	</ul>
</div>
</template>

<script>
import axios from 'axios'
export default {
	name: 'BrewList',
	data(){
		return{
			brews:[]
		}
	},
	mounted(){
    axios.get('https://api.openbrewerydb.org/breweries/').then(response=>  this.brews = response.data)
  }
}
</script>

<style lang="scss" scoped>
.brew-list{
    overflow-y: scroll;
    height: 95vh;
    li {
      &:hover {
        background-color: darkgray;
      }
    }
  }
</style>