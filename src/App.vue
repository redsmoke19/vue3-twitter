<script setup>
import { onMounted, ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router'

const tweetList = ref([]);

onMounted(() => {
  document.title = "Приложение v-twitter";
  getTweets();
});

const getTweets = () => {
  const localTweets = localStorage.getItem("tweets");
  if (localTweets) {
    tweetList.value = JSON.parse(localTweets);
  }
}

const handleGetTweet = (tweet) => {
  tweetList.value.push(tweet);
}

watch(tweetList,
  (val) => {
    localStorage.setItem("tweets", JSON.stringify(val));
  },
  { deep: true }
)
</script>

<template>
  <div class="wrapper">
    <header class="header">
      <div class="header__wrapper container">
        <nav class="main-nav">
          <RouterLink to="/" class="main-nav__link">Home</RouterLink>
          <RouterLink to="/about" class="main-nav__link">About</RouterLink>
        </nav>
        <span class="header__logo">v-twitter</span>
      </div>
    </header>

    <RouterView :tweetList="tweetList" @on-get-tweet="handleGetTweet" />
  </div>
</template>

<style lang="scss" scoped>
.wrapper {
  // height: 100vh;
  padding: 110px 0 160px;
}
.header {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  margin: 0 0 40px 0;
  background-color: #fff;
  z-index: 10;
  box-shadow:
    0 1px 1px hsla(217, 86%, 73%, 0.075),
    0 2px 2px hsla(217, 86%, 73%, 0.075),
    0 4px 4px hsla(217, 86%, 73%, 0.075),
    0 8px 8px hsla(217, 86%, 73%, 0.075),
    0 16px 16px hsla(217, 86%, 73%, 0.075);
  padding: 20px 0;

  &__wrapper {
    display: grid;
    align-items: center;
    grid-template-columns: repeat(3, 1fr);
  }

  &__logo {
    text-align: center;
    font-size: 50px;
    line-height: 1;
    color: #00aced;
  }
}

.main-nav {
  display: flex;
  align-items: center;

  &__link {
    font-size: 25px;
    line-height: 1;
    text-decoration: none;
    color: #1dcaff;
    transition: opacity 0.3s ease-out;

    &:hover {
      opacity: 0.7;
    }

    &.router-link-active {
      text-decoration: underline;
      color: #97cfea;
    }

    &:not(:last-child) {
      margin: 0 15px 0 0;
    }
  }
}

.main-nav {
  display: flex;
}
</style>
