<template>
    <div id="app">
        <VSelect v-model="value"
                  :options="options"
                  selectName="name"
                  selectKey="code"
                  @change="onChange"
        ></VSelect>
    </div>
</template>
<script>

//import VSelect from '../dist/vue-select.min.js'
import vSelect from '../src/index'
export default {
  components: {
    'VSelect': vSelect
  },
  data () {
    return {
        options: [
            {name:'hello',code:1},
            {name:'my',code:2},
            {name:'name',code:3},
            {name:'is',code:4},
            {name:'gao',code:5},
            {name:'shuai',code:6}
        ],
        value: 1
    }
  },
  mounted() {
      var vm = this;
      setTimeout(()=> {
          vm.options = [
              {name:'hello',code:1},
              {name:'my',code:2},
              {name:'name',code:3},
              {name:'is',code:4},
              {name:'gao',code:5},
              {name:'shuai',code:6},
              {name:'a Web Engineer',code:7},
              {name:'happy New Year',code:8},
              {name:'a Web Engineer',code:9},
              {name:'happy New Year',code:10},
              {name:'a Web Engineer',code:11},
              {name:'happy New Year',code:12}
          ]
      },5000)
  },
  methods: {
      onChange: function () {
          console.log(this.value)
      }
  },

}
</script>

<style lang="stylus">
    html,body{
        height: 100%;
        overflow: hidden;
        padding: 0;
        margin: 0;
    }
   #app{
       width: 100%;
       height: 100%;
       background: #fefbfc;
   }
</style>
