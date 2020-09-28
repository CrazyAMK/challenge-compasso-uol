<template>
  <div v-if="data.length != 0" class="user-details mt-5">
    <h2>User details</h2>
    <div class="row flex-row-reverse">
      <div class="col-sm-6 align-self-center">
        <div class="col-12 avatar_img m-auto pb-2">
          <img :src="data.avatar_url" :alt="data.name" />
        </div>
      </div>
      <ul class="col-sm-6 align-self-center mb-3 list-group-flush">
        <li class="col-12 list-group-item" v-if="data.name">
          <b>Name:</b> {{ data.name }}
        </li>
        <li class="col-12 list-group-item" v-if="data.login">
          <b>Username:</b> {{ data.login }}
        </li>
        <li class="col-12 list-group-item" v-if="data.company">
          <b>Company:</b> {{ data.company }}
        </li>
        <li class="col-12 list-group-item" v-if="data.blog">
          <b>Blog:</b>
          <a :href="'https://' + data.blog" target="_blank">{{ data.blog }}</a>
        </li>
        <li class="col-12 list-group-item" v-if="data.location">
          <b>Location:</b> {{ data.location }}
        </li>
        <li class="col-12 list-group-item" v-if="data.twitter_username">
          <b>Twitter:</b>
          <a
            :href="'https://twitter.com/' + data.twitter_username"
            target="_blank"
            >@{{ data.twitter_username }}</a
          >
        </li>
      </ul>
    </div>

    <Buttons :username="data.login"></Buttons>
  </div>
  <div v-else-if="data.length == 0">
    <p class="alert alert-danger" role="alert">{{ errorsMsg }}</p>
  </div>
</template>

<script>
import Buttons from "./Buttons.vue";
export default {
  components: { Buttons },
  props: {
    data: {
      required: true,
    },
    errorsMsg: {
      default: "User not found",
    },
  },
};
</script>

<style scoped>
.avatar_img {
  max-width: 300px;
}

.avatar_img img {
  max-width: 100%;
}
</style>