<template>

      <title>Product App</title>
      <div class="nav-bar"></div>

      <div id="app">
          <div class="cart">
              <p>Cart({{ cart.length }})</p>
          </div>

        <ProductItem 
          @add-to-cart="updateCartAdd" 
          @remove-from-cart="updateCartRemove">
          </ProductItem>
     
      </div>

</template>

<script>

import ProductItem from './components/ProductItem'

export default {
  name: 'App',
  components: {
    ProductItem
    },
   data () {
     return {
       cart: []
     }
    },
    methods: {
        updateCartAdd(id){
            this.cart.push(id)
        },
        updateCartRemove(id){
            this.cart.pop(id)
        }
    }
}
</script>

<style>
body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
  }
  
  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  
  .cart {
    display: flex;
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }

/* Can component properties be defined like this? */
  .ProductItem {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
