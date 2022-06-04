<template>
    <div class="product">

      <div class="product-image">
            <img :src="image">
            </div>
      
      <div class="product-info">
          <h1>{{ productTitle }}</h1>
          <p v-if="inStock">In Stock</p>
          <p v-else>Out of stock</p>
      
          <div class="color-box" 
              v-for="(variant, i) in variants" 
              :key="variant.variantId"
              :style="{ backgroundColor: variant.variantColor }"
              @mouseover="updateProduct(i)">
          </div>

        </div>

    </div>

    <button @click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
        >Add to cart</button>
    <button @click="removeFromCart">Remove from cart</button>

    <ProductTabs :reviews="reviews"></ProductTabs>
</template>

<script>
import ProductTabs from './ProductTabs.vue'

export default {
  components: {
        ProductTabs
    },
    data() {
        return {
            brand: "MPCo",
            product: "Medias",
            selectedVariant: 0,
            variants: [
                {
                    variantId: 2022060301,
                    variantColor: "green",
                    variantImage: "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
                    variantQuantity: 4,
                },
                {
                    variantId: 2022060302,
                    variantColor: "blue",
                    variantImage: "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
                    variantQuantity: 3,
                }
            ],
            reviews: []
        };
    },
    methods: {
        addToCart() {
            this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
            this.variants[this.selectedVariant].variantQuantity--
        },
        removeFromCart() {
            this.$emit("remove-from-cart", this.variants[this.selectedVariant].variantId);
            this.variants[this.selectedVariant].variantQuantity++
        },
        updateProduct(index) {
            this.selectedVariant = index;
        },

    },
    computed: {
        productTitle() {
            return this.brand + " " + this.product;
        },
        image() {
            return this.variants[this.selectedVariant].variantImage;
        },
        inStock() {
            return this.variants[this.selectedVariant].variantQuantity;
        },
        
    },
}

</script>


<style>
    body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
    display: flex;
  } 

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 70%;
    margin: 0px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  .product-image {
    width: 50%;
    flex-basis: 400px;
  }
  
  .product-info {
    margin-top: 10px;
    /* width: 50%; */
    flex-basis: 300px;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin: 5px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
  
  .disabledButton {
    background-color: #d8d8d8;
  }

</style>