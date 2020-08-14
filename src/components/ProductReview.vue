<template>
<div> 
    <div>Product review</div>
      <p v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="(error,index) in errors" :key="index">{{ error }}</li>
      </ul>
    </p>
    <form class="review-form" @submit.prevent="onSubmit">
        <p>
            <label for="name">Name:</label>
            <input id="name" v-model="productReview.name"/>
        </p>
         <p>
            <label for="review">Review:</label>
            <textarea id="review" v-model="productReview.review"/>
        </p>
         <p>
            <label for="rating">Rating:</label>
            <select id="rating" v-model.number="productReview.rating">
                <option>5</option>
                <option>4</option>
                <option>3</option>
                <option>2</option>
                <option>1</option>
            </select>
        </p>
         <div>
            <p for="recomended">Recomend:</p>
            <label><input type="radio" v-model="productReview.recomended" :value="true">Yes</label>
            <label><input type="radio" v-model="productReview.recomended" :value="false">Not</label>
          </div>
        <p>
        <input type="submit" value="Submit">  
      </p>  
    </form>
    </div>
</template>
<script>
import { eventBus } from '../eventBus.js';

export default {
    name:'ProductReview',
    data:function(){
        let productReview={
                name:'',
                review:'',
                rating:null,
                recomended:null,
            };
        return {
               productReview,
               errors:[] 
        }
    },
    methods:{
        onSubmit(){
             
            if (this.productReview.name && this.productReview.review && this.productReview.rating){
                let clonedReview=Object.assign({}, this.productReview);
            //this.$emit('add-review',clonedReview);
            eventBus.$emit('add-review',clonedReview);
            this.productReview.name='';
            this.productReview.review='';
            this.productReview.rating=null;
            this.productReview.recomended=null;
            this.errors=[];
            }
            else{
                if (!this.productReview.name) {this.errors.push('name is required');}
                if (!this.productReview.review) {this.errors.push('review is required');}
                if (!this.productReview.rating) {this.errors.push('rating is required');}
                 if (!this.productReview.recomended) {this.errors.push('recomended is required');}
            }

        }
    }
}
</script>