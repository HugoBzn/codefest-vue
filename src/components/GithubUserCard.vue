<template>
  <div class="ui card">
    <div class="image">
      <a class="ui green ribbon label">Vue 3 Codefest2022 😎</a>
      <img :src="'http://localhost:1337' + image.url" />
    </div>
    <div class="content">
      <a class="header">{{ user.name }}</a>
      <div class="meta">
        <span class="date">{{ user.createdAt }}</span>
      </div>
      <div class="description">
        {{ user.bio }}
      </div>
    </div>
    <div class="extra content">
      <a>
        <i class="user icon"></i>
        {{ user.followers }}
      </a>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
const props = defineProps({
  username: {
    type: String,
    required: true,
    default: "No name",
  },
});

const user = ref("");
const image = ref("");

// Solicitando datos
const id = props.username;
// Version con Promesas
// axios.get(`https://api.github.com/users/${name}`).then((res) => {
//   user.value = res.data;
//   user.value["created_at"] = new Date(user.value["created_at"]).toDateString();
// });

/* Version con Async Await */
(async function () {
  const res = await axios.get(`http://localhost:1337/api/github-profiles/${id}/?populate=*`);
  user.value = res.data.data.attributes;
  image.value = res.data.data.attributes.avatar_image.data.attributes.formats.thumbnail;
  user.value["createdAt"] = new Date(user.value["createdAt"]).toDateString();
})();
</script>
