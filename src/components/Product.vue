<template>
          <div class="product"> 
        <div class="product-image">
          <img :src="image" :alt="description" :style="{width:'350px'}" />
        </div>
        <div>cartNumberItems {{cartNumberItems}}</div>
        <div class="product-info">
          <h1>{{title}}</h1>
          <p v-if="inventory>10">In stock</p>
          <p v-else-if="inventory<=10 && inventory>0">Almost out stock</p>
          <p v-else :style="{textDecoration:'line-through',color:'red'}">Out of stock</p>
            <p>Shipping {{shipping}}</p>
          <span v-show="onSale">{{onSaleText}}</span>
          <!-- <ul>
            <li v-for="(detail, index) in details" :key="index">{{detail}}</li>
          </ul> -->
          <ProductDetails :details="details"></ProductDetails>
          <div>
            <div>Available variants</div>
            <div
              v-for="(variant, index) in variants"
              :key="index"
              class="color-box"
              :style="{backgroundColor:variant.variantColor,color:'red'}"
            >
              <p  @mouseover="updateProduct(index)"  >{{variant.variantColor}}</p>
               <!-- @mouseleave="updateProduct(mainVariantId)" -->
            </div>
          </div>
          <div>
            <div>Available sizes</div>
            <p v-for="(size, index) in sizes" :key="index">{{size}}</p>
          </div>
 

          <div class="product-link">
            <a :href="link" target="_blank">Link to product</a>
          </div>
 <div class="cartButtons">
        <button
          @click="addToCart"
          :disabled="!inStock"
          :class="{disabledButton:!inStock}"
        >Add to cart</button>
              <button
          @click="deleteFromCart"
          :disabled="cartNumberItems==0"
          :class="{disabledButton:!cartNumberItems}"
          :style="{marginLeft:'5px',marginRight:'5px'}">Delete to cart</button>
        </div>
        <div style="{clear:'both'}">

       <div>
         <ProductTabs :reviews="reviews" @add-review="addReview"></ProductTabs>
       </div>
          
        </div>
        </div>
         
      </div>
</template>
<script>
import { eventBus } from '../eventBus.js';

import ProductDetails from '@/components/ProductDetails';
// import ProductReview from '@/components/ProductReview';
import ProductTabs from '@/components/ProductTabs';
 export default {
    name:'Product',
    components:{
        ProductDetails,
        //ProductReview,
        ProductTabs
    },
    props:{
        premium:{
            type:Boolean,
         required:true,
        },
        cartNumberItems:{
            type:Number,
            required:true
        }
    },
  
     data: function () {
    return {
      brand: "thesockmafia",
      product: "Socks",
      mainVariantId:1000,
      selectedVariant:1000,
      baseImage: "./assets/green.jpg",
      //    image:"https://www.thesockmafia.com/uploads/b/77cdc480-5ca8-11e9-beb6-eba16cb6daaa/e42aef80-04cc-11ea-9f40-599e59e14257.jpg",
      link: "https://www.thesockmafia.com/",
      description: "sock image",
      inventory: 100,
      // inStock: this.inventory > 0,
      onSale: true,
      details: ["80% cotton", "20% polyester", "Gender femaile"],
      reviews:[],
      variants: [
        {
          variantId: 2234,
          variantColor: "yellow",
          variantQunatity: 10,
          variantImage: "./assets/yellow.jpeg",
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantQunatity: 5,
          variantImage: "./assets/blue.jpeg",
        },
      ],
      sizes: ["S", "M", "L"] 
    };
  },
  methods: {
    addToCart: function () {
     // this.cart += 1;
     this.$emit('add-to-cart',this.selectedVariant);
    },
    deleteFromCart:function(){
       this.$emit('remove-from-cart',this.selectedVariant);  
    },
    updateProduct: function (index) {
      this.selectedVariant = index;
       console.log(this.selectedVariant);
    },
    addReview: function (review) {
        
        console.log(review.name);
        console.log(review.review);
        console.log(review.rating);
         debugger; // eslint-disable-line
     this.reviews.push(review);
     console.log(this.reviews);
    },
     
  },
  computed: {
    title: function () {
      return this.brand + " " + this.product;
    },
    onSaleText:function(){
      if (this.onSale){
        return this.brand+' ' +this.product+ 'On Sale';
      }
      else{
           return this.brand+' ' +this.product ;
      }
    },
    shipping:function(){
         return (this.premium)?"Free":"2.99$"; 
    },
    inStock:function(){
    if (this.selectedVariant != this.mainVariantId) {
        return this.variants[this.selectedVariant].variantQunatity;
      } else {
        return this.inventory>0;
      }
    },
    image: function () {
      if (this.selectedVariant != this.mainVariantId) {
        return this.variants[this.selectedVariant].variantImage;
      } else {
        return this.baseImage;
      }
    },
  },
   mounted() {
        eventBus.$on('add-review', productReview => {
          this.reviews.push(productReview)
        })
      }
}
</script>
<style scoped>

</style>