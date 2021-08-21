<template>
  <div class="contain">
    <div
      class="
        urlshortener
        w-full
        bg-purple-50 bg-cover bg-no-repeat bg-center
        object-cover
      "
    >
      <form @submit.prevent="shortenUrl" class="text-center py-56">
        <input
          type="text"
          name="urls"
          id="url"
          v-model="urltoshorten"
          placeholder="Enter URL to shorten .."
          class="
            py-4
            px-20
            text-center
            rounded
            focus:outline-none
            bg-white bg-opacity-80
          "
        />
      </form>
    </div>
    <div class="copy py-16 text-center">
      <h4 class="text-3xl text-center py-6 rounded inline pr-10">
        {{ shorturl }}
      </h4>
      <button type="button" class="text-xl w-8 h-8">
        <img src="./assets/clapping.svg" alt="My Happy SVG" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      urltoshorten: "",
      shorturl: "",
    };
  },
  methods: {
    shortenUrl() {
      // send a POST request
      const url = new URL("https://t.ly/api/v1/link/shorten");

      let headers = {
        "Content-Type": "application/json",
        Accept: "application/json",
      };

      let body = {
        long_url: this.urltoshorten,
        domain: "https://t.ly/",
        api_token: "",
      };

      fetch(url, {
        method: "POST",
        headers: headers,
        body: JSON.stringify(body),
      })
        .then((response) => response.json())
        .then((data) => {
          this.shorturl = data.short_url;
          console.log(data);
        });
      this.urltoshorten = "";
    },
    // copy link method
  },
};
// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/master/active-rfcs/0040-script-setup.md
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.urlshortener {
  background-image: url("https://images.unsplash.com/photo-1607458640068-95c63d96f779?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80");
  height: 500px;
}
</style>
