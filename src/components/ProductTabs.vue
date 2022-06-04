<template>
      <div>
            <span class="tab"
                :class="{ activeTab: selectedTab === tab}"
                v-for="(tab, i) in tabs"
                :key="i"
                @click="selectedTab = tab">
                {{ tab }}</span>
        </div>
        <div v-show="selectedTab === 'Reviews'">
            <h2>Review</h2>
            <p v-if="!reviews.length">There are no reviews yet.</p>
            <ul>
                <li v-for="(review, i) in reviews"
                :key="i">
                <p>{{ review.name }}</p>
                <p>{{ review.rating }}</p>
                <p>{{ review.review }}</p>
                </li>
            </ul>
            </div>
        <div>

            <ProductReview v-show="selectedTab === 'Create a review'"
            ></ProductReview>

        </div>
</template>

<script>
import ProductReview from './ProductReview'
export default {
    components: {
        ProductReview
    },
    props: {
        reviews: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            tabs: ["Reviews", "Create a review"],
            selectedTab: "Reviews"
        };
    }
}
</script>


<style>

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }


</style>
