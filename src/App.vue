<script setup>
import GithubUserCard from "./components/GithubUserCard.vue";
// Referencia reactiva
import { ref } from "vue";

const users = ref(["1", "2"]);
</script>

<template>
  <div id="app" class="ui container">
    <h1>GitHub Profiles</h1>
    <div class="ui cards">
      <GithubUserCard v-for="user in users" :username="user" />
    </div>
  </div>
</template>
