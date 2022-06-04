<template>
     <form class="review-form" @submit.prevent="onSubmit">

    <p v-if="errors.length">
        <b>Please correct:</b>
        <ul>
            <li v-for="(error, i) in errors"
            :key="i"
            >{{ error }}</li>
        </ul>
    </p>

    <p>
        <label for="name">Name:</label>
        <input id="name" v-model="name">
    </p>

    <p>
        <label for="review">Review:</label>      
        <textarea id="review" v-model="review"></textarea>
    </p>

    <p>
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
        </select>
    </p>

    <p>Would you recommend this product?</p>      
        <label>
            yes
            <input type="radio" value="yes" v-model="rec">
        </label>
        <label>
            no
            <input type="radio" value="no" v-model="rec">
        </label>

    <p>
        <input type="submit" value="Submit">  
    </p>    

    </form>
</template>

<script>
export default {
    data(){
        return {
            name: null,
            review: null, 
            rating: null,
            rec: false,
            errors: []
        }
    }, 
    methods: {
        onSubmit() {
            if(this.name && this.review && this.rating && this.rec){
                let productReview = {
                    name: this.name,
                    review: this.review,
                    rating: this.rating,
                    rec: this.rec
                }
                this.$emit('review-submitted', productReview)
                this.name = null
                this.review = null
                this.rating = null
                this.rec=null
            } else {
                if(!this.name) this.errors.push("Name required.")
                if(!this.review) this.errors.push("Review required.")
                if(!this.rating) this.errors.push("Rating required.")
                if(!this.rec) this.errors.push("Rec/not rec required.")
            }
        }
    }
}
</script>


<style>
  
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
</style>