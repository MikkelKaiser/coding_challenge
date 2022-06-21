<template>
  <div class="home">
    <h1>Home Page</h1>
    <div v-for="story in stories" :key="story">
    <h2>{{story.data.title}}</h2>
    <p>Url: {{story.data.url}}</p>
    <p>Comments: {{story.data.descendants}}</p>
    <p>Score: {{story.data.score}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

  export default {
    name: "HomeView",
    data: function () {
      return {
        err: '',
        stories: [],
      }
    },
    created: function () {
      // Make request to the API
      // https://hacker-news.firebaseio.com/v0/topstories.json
      axios.get('https://hacker-news.firebaseio.com/v0/topstories.json')
      .then((response) => {
        // Get the 10 first stories response and populate it to the stories array
        let results = response.data.slice(0, 10);
        results.forEach(id => {
          axios.get('https://hacker-news.firebaseio.com/v0/item/' + id + '.json')
          .then((response) => {
            this.stories.push(response);
          })
          .catch((err) => {
            this.err = err;
          })
        })
      })
      .catch((err) => {
        // If fails catch the error
        this.err = err;
      })

    },

  };
</script>

<style lang="scss" scoped>
.home {
  position: absolute;
  margin-top: 200px;
  width: 100%;
  height: 100%;
}
</style>