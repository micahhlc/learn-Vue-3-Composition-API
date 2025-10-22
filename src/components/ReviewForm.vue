<script setup>
  import { ref, reactive } from 'vue';

  const emit = defineEmits(['review-submitted']);

  const review = reactive({
    name: '',
    content: '',
    rating: null,
  });

  let alertMsg = ref('');
  let alertTimer = 2000;

  const onSubmit = () => {
    if (review.name === '' || review.content === '' || review.rating === null) {
      alertMsg.value = 'Plst fill out all info.';
      console.log(alertMsg.value);
      setTimeout(() => {
        alertMsg.value = '';
      }, 5000);
      console.log('after 5s: ', alertMsg.value);
      // console.log(review);
      return;
    }
    const productReview = {
      name: review.name,
      content: review.content,
      rating: review.rating,
    };
    emit('review-submitted', productReview);
    alertMsg.value = '';
    review.name = 'kk';
    review.content = '';
    review.rating = null;
  };
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <!-- <p :class="{ 'alert-msg': alertMsg.length > 0 }">{{ alertMsg }}</p> -->
    <transition name="fade">
      <p v-if="alertMsg.length" class="alert-msg">{{ alertMsg }}</p>
    </transition>

    <label for="name">Name:</label>
    <input id="name" v-model="review.name" />

    <label for="review">Review:</label>
    <textarea id="review" v-model="review.content"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="review.rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <input class="button" type="submit" value="Submit" />
  </form>
</template>
