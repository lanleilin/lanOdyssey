<template>
  <div class="comtainer">
      <p>this is static</p>
      <a class="img-items" v-for='(item,index) in anchorList' :key="index" :href="item.url" target="blank"> {{ item.name }} </a>
  </div>
</template>
<script>
export default {
  data(){
    return{
      anchorList:[{
        name:'vue',
        url:'https://www.baidu.com'
      },{
        name:'baidu',
        url:'https://www.baidu.com'
      }
      ]
    }
  }
  
}
</script>
<style scoped>
a{
  text-decoration: none;
  padding:3px 4px;
  margin: 3px 4px;
  border: 1px solid lightsalmon;
  border-radius: 2px;
}
</style>


