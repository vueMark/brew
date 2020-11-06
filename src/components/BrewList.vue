<template>
  <div class="card brew-list">
    <ul class="list-group list-group-flush">
      <li class="list-group-item" v-for="(brew,index) in brews" :key="index">{{brew.name}}, {{brew.state}}</li>
      </ul>
</div>
</template>

<script>

export default {
	name: 'BrewList',
	data(){
		return{

		}
  },
  props:{
    brews:Array
  }
}
</script>

<style lang="scss" scoped>
.brew-list{
    overflow-y: scroll;
    height: 80vh;
    li {
      &:hover {
        background-color: darkgray;
      }
    }
  }
</style>