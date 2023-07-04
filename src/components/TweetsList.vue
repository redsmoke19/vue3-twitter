<script setup>
import { ref, computed } from 'vue';
import TweetItem from './TweetItem.vue';

const props = defineProps({
  tweetList: {
    type: Array,
    required: true,
  }
})

const sortBy = ref("date");

const sorteredItems = computed(() => {
  return [...props.tweetList].sort((a, b) => {
    if (a[sortBy.value] > b[sortBy.value]) return -1
    if (a[sortBy.value] < b[sortBy.value]) return 1
  })
})

</script>

<template>
  <select class="select" v-model="sortBy" name="sort">
    <option value="date">Sort by date</option>
    <option value="likes">Sort by likes</option>
  </select>
  <div class="tweets">
    <ul class="tweets__list">
    <tweet-item v-for="tweet in sorteredItems" :key="tweet.id" :tweet="tweet" />
  </ul>
  </div>
</template>

<style lang="scss">
.tweets {
  &__list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: grid;
    gap: 40px;
  }
}

.select {
  font-size: 20px;
  padding: 10px;
  border-radius: 20px;
  font-family: inherit;
  display: grid;
  appearance: none;
  position: fixed;
  right: 20px;
  top: 25px;
  z-index: 44;

  &::after {
    content: "";
    width: 20px;
    height: 10px;
    background-color: #00aced;
    clip-path: polygon(100% 0%, 0 0%, 50% 100%);
  }

  &::-ms-expand {
    display: none;
  }
}
</style>