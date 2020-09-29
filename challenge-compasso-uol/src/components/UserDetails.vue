<template>
  <div v-if="data.length != 0" class="user-details mt-5">
    <h2>{{ data.name }}</h2>
    <hr />
    <div class="row flex-row-reverse">
      <div class="col-sm-6 align-self-center">
        <div class="col-12 avatar_img m-auto pb-2">
          <img :src="data.avatar_url" :alt="data.name" />
          <a
            :href="data.html_url"
            target="_blank"
            class="btn btn-outline-success w-100 mt-2"
            >Visit profile</a
          >
        </div>
      </div>
      <ul class="col-sm-6 align-self-center mb-3 list-group-flush">
        <li class="col-12 list-group-item" v-if="data.login">
          <b>Username:</b> {{ data.login }}
        </li>
        <li class="col-12 list-group-item" v-if="data.company">
          <b>Company:</b> {{ data.company }}
        </li>
        <li class="col-12 list-group-item" v-if="data.email">
          <b>Email:</b> {{ data.email }}
        </li>
        <li class="col-12 list-group-item" v-if="data.blog">
          <b>Blog:</b>
          <a :href="data.blog" target="_blank">{{ data.blog }}</a>
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
        <li class="col-12 list-group-item" v-if="data.location">
          <b>Member Since:</b> {{ data.created_at }}
        </li>
        <li class="col-12 list-group-item">
          <span class="badge badge-dark">
            Public Repos: {{ data.public_repos }}
          </span>
          <span class="badge badge-info">
            Public Gists: {{ data.public_gists }}
          </span>
          <span class="badge badge-success">
            Followers: {{ data.followers }}
          </span>
          <span class="badge badge-danger">
            Following: {{ data.following }}
          </span>
        </li>
      </ul>
    </div>
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

ul li:first-child {
  border-top: 0;
}
</style>