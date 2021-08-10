<template>
  <app-select
          :options="options"
          @select="optionSelect"
          :selected="selected"
  ></app-select>
  <h1>Вы выбрали: {{selected}}</h1>
</template>

<script>
import AppSelect from './components/AppSelect.vue'

export default {
  name: 'App',
  data() {
    return{
      options:[
        {name: 'option 1', value: 1},
        {name: 'option 2', value: 2},
        {name: 'option 3', value: 3},
        {name: 'option 4', value: 4},
        {name: 'option 5', value: 5}
      ],
      selected: 'Опции'
    }
  },
  methods:{
    optionSelect (option){
      this.selected = option.name
    }
  },
  components: {
    AppSelect
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
