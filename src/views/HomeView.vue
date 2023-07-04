<script setup>
import AppForm from "../components/AppForm.vue"
import TweetsList from "../components/TweetsList.vue";

const emit = defineEmits(["onGetTweet"])

defineProps({
  tweetList: {
    type: Array,
    required: true,
  }
})

const handleFormSubmit = (tweet) => {
  emit("onGetTweet", tweet);
}
</script>

<template>
  <main>
    <div class="container">
      <app-form @on-form-submit="handleFormSubmit"/>
      <tweets-list :tweetList="tweetList" />
    </div>
  </main>
</template>
