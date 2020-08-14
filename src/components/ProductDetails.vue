<template>
          <div class="product-details"> 
          <ul>
            <li v-for="(detail, index) in details" :key="index">{{detail}}</li>
          </ul>
           </div>
</template>
<script>
export default {
    name:'Product-Details',
    props:{
        details:{
          type:Array,
          required:true,
        }
    }, 
  methods: {
     
  },
  computed: {
    
  }
}
</script>
<style scoped>

</style>