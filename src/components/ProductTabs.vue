<template>
<div>
    <div>ProductTabs </div>
        <ul>
            <span  :class="{ activeTab: selectedTab === tab }"
                  v-for="(tab, index) in tabs"  :key="index"
                  @click="selectedTab = tab" 
            >{{ tab }}</span>
          </ul> 
           <div v-show="selectedTab === 'Review'"> 
                 <p v-if="!reviews && !reviews.length">There are no reviews yet.</p>
                <ul>
                    <li v-for="(review,index) in reviews" :key="index">
                      <p>Name :{{ review.name }}</p>
                      <p>Rating:{{ review.rating }}</p>
                      <p> Review: {{ review.review }}</p>
                       <p> Recomended: {{ review.recomended }}</p>
                    </li>
                </ul>
            </div>   
 <div v-show="selectedTab === 'Make a Review'">  
   <ProductReview></ProductReview>
</div>

</div>
</template>
<script>
import ProductReview from '@/components/ProductReview';
export default {
    name:'ProductTabs',
    props:{
        reviews:Array
    },
    components:{
        ProductReview
    },
    data:function() {
        return {
          tabs: ['Review', 'Make a Review'] ,
          selectedTab: 'Review'  // set from @click
     
        }
      }
}
</script>
<style scoped>

</style>