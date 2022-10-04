<template>
    <div class="ReviewContainer">
        <div v-for="review in this.$store.state.reviews" v-bind:key="review.reviewId">
            <div id="review-info">
                <h3>Rating: {{ review.rating }}</h3>
                <p>Review: {{ review.description }}</p>
            </div>
        </div>
    </div>
</template>