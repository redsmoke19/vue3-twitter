<script setup>
defineProps({
  tweet: {
    type: Object,
    required: true,
  }
})
</script>

<template>
<li class="tweets__item">
  <img :src="tweet.avatar" alt="Изображение пользователя" width="80" height="80" class="tweets__img">
  <div class="tweets__wrapper">
    <span class="tweets__date">{{ tweet.date }}</span>
  <p class="tweets__body">{{ tweet.text }}</p>
  <p class="tweets__likes">♥️ {{ tweet.likes }}</p>
  </div>
</li>
</template>

<style lang="scss">
.tweets {
  &__item {
    display: flex;
    background-color: rgba(#eeeeee, 0.5);
    padding: 20px;
    border-radius: 15px;
    align-items: center;
  }

  &__img {
    display: flex;
    margin: 0 30px 0 0;
  }

  &__wrapper {
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  &__body {
    max-width: 60%;
  }

  &__date,
  &__likes {
    display: flex;
    align-self: flex-end;
    opacity: 0.6;
    margin: 0;
  }
}
</style>
