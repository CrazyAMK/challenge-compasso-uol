<template>
  <div>
    <div v-if="repos.length != 0" class="results mt-5">
      <slot name="title">Repositories</slot>
      <hr />
      <ul class="mt-4 list-group list-group-flush">
        <li v-for="repo in repos" class="col-12 m-0">
          <a
            :href="repo.html_url"
            target="_blank"
            class="list-group-item list-group-item-action d-md-flex"
          >
            <div class="col-md-6">
              {{ repo.name }}
            </div>
            <div class="col-md-6 text-md-right">
              <span class="badge badge-dark">
                Forks: {{ repo.forks_count }}
              </span>
              <span class="badge badge-info">
                Watchers: {{ repo.watchers_count }}
              </span>
              <span class="badge badge-success">
                Stars: {{ repo.stargazers_count }}
              </span>
            </div>
            <div></div>
          </a>
        </li>
      </ul>
    </div>
    <div v-else-if="errors.length" class="mt-5">
      <slot name="title">Repositories</slot>
      <hr />
      <p class="alert alert-danger" role="alert">{{ errors }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repos", "errors"],
};
</script>

<style scoped>
ul {
  list-style: none;
}
ul li:first-child a {
  border-top: none;
}
</style>