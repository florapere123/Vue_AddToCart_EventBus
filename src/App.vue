<template>
  <div class="main">
    <div class="nav-bar"></div>
    <div id="app">
      
       <div class="cart">
          <p>Cart ({{cart.length}})</p>
        </div>
 <product  :premium="premium" :cartNumberItems="cart.length" @add-to-cart="updateCart" @remove-from-cart="removeItem"  ></product>
    </div>
  </div>
</template>

<script>
import Product from './components/Product';
 export default {
  name: "App",
  components: {Product},
   data:function(){
     return {
       premium:true,
       cart:[]
     }
   },
   methods: {
  
    updateCart: function (id) {
        debugger; // eslint-disable-line 
       this.cart.push(id);
       
       console.log(this.cart.length)
        debugger; // eslint-disable-line
    },
      removeItem: function (id) {
         
          for(var i = this.cart.length - 1; i >= 0; i--) {
            if (this.cart[i] === id) {
               this.cart.splice(i, 1);
            }
          }
        }
   }
};
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
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>
