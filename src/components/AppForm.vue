<script setup>
import { ref } from 'vue';

const emit = defineEmits(["onFormSubmit"]);
const tweet = ref("");

const handleSubmit = () => {
  const newTweet = {
    id: Math.random().toString(36).substring(2, 100),
    avatar: `https://api.dicebear.com/6.x/adventurer/svg?seed=${Date.now()}`,
    text: tweet.value,
    likes: Math.floor(Math.random() * 1000),
    date: new Date(Date.now()).toLocaleString(),
  }
  emit("onFormSubmit", newTweet);

  tweet.value = "";
}
</script>

<template>
  <form class="form" @submit.prevent="handleSubmit">
    <textarea class="form__textarea" v-model="tweet" required placeholder="Type tweet here"></textarea>
    <button class="form__button" type="submit">Submit</button>
  </form>
</template>

<style lang="scss">
.form {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(#00aced, 0.5);
  padding: 20px 30px;
  display: flex;
  z-index: 20;

  &__textarea {
    flex-grow: 1;
    resize: none;
    height: 100px;
    border: none;
    border-radius: 20px 0 0 20px;
    padding: 20px;
    font-size: 18px;
    line-height: 1.2;
    font-family: inherit;
  }

  &__button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 150px;
    border: none;
    border-radius: 0 20px 20px 0;
    font-size: 30px;
    line-height: 1;
    background-color: #00aced;
    color: #fff;
    font-family: inherit;
    cursor: pointer;
    transition: opacity 0.3s ease-out;

    &:hover {
      opacity: 0.7;
    }
  }
}
</style>