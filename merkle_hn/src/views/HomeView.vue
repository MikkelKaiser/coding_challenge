<template>
  <section class="stories">
    <div v-for="story in sortedArray" :key="story">
      <div class="story" @mousemove="mousemove">
        <div class="story-inner">
          <div class="story-image-wrap">
            <div class="story-text-wrap">
              <h2 class="bg-text">{{ story.data.title }}</h2>
            </div>
            <img src="../assets/merkle_logo.png" class="image" alt="">
          </div>
          <div class="story-detail">

            <h2>{{ story.data.title }}</h2>
            <p>Author: {{ story.data.by }}</p>
            <p>Url: {{ story.data.url }}</p>
            <p>Time: {{ story.data.time }}</p>
            <p>Score: {{ story.data.score }}</p>

          </div>
        </div>
      </div>
    </div>
  </section>
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
    axios.get('https://hacker-news.firebaseio.com/v0/topstories.json')
      .then((response) => {
        // Get the 10 first stories response and populate it to the stories array
        let results = response.data.slice(0, 10);
        results.forEach(id => {
          axios.get('https://hacker-news.firebaseio.com/v0/item/' + id + '.json')
            .then((response) => {
              this.stories.push(response);
              // let newStory = Object.assign(this.stories, {story: response.data}) 
              let authorId = response.data.by;
              axios.get('https://hacker-news.firebaseio.com/v0/user/' + authorId + '.json')
                .then((response) => {
                  // newStory = Object.assign(this.stories, {author: response.data}) 
                  console.log(response)
                })

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
  methods: {
    mousemove(e) {
      let mouseX = e.clientX;
      let mouseY = e.clientY;

      let stories = document.querySelectorAll('.stories .story');
      for (let i = 0; i < stories.length; i++) {
        let story = stories[i];

        let story_image = story.querySelector('.story-image-wrap');

        let img_x = mouseX - this.coords(story_image).x;
        let img_y = mouseY - this.coords(story_image).y;

        story_image.style.transform = `translateY(-${img_y / 45}px) translateX(-${img_x / 45}px) translateZ(100px)`;


        let bgtext = story.querySelector('.bg-text');
        let bg_x = mouseX - this.coords(bgtext).x;
        let bg_y = mouseY - this.coords(bgtext).y;
        bgtext.style.transform = `translateX(${bg_x / 25}px) translateY(${bg_y / 25}px)`
      }
    },
    coords(el) {
      let coords = el.getBoundingClientRect();
      return {
        x: coords.left / 2,
        y: coords.top / 2,

      }
    },
  },

  computed: {
    sortedArray: function () {
      return [...this.stories].sort((a, b) => a.data.score - b.data.score);
    }
  },

};
</script>

<style lang="scss" scoped>
.story {
  // flex: 1 1 33.333%;
  width: 100%;
  padding: 25px;

  .story-inner {
    position: relative;
    padding: 25px;
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-image: linear-gradient(to bottom right, #24D484, #116432);

    .story-detail {
      background-color: #fff;
      padding: 25px;
      margin: 0px -25px -25px;
      overflow: hidden;

      h2 {
        font-size: 24px;
        font-weight: 700;
        color: #676767;
        margin-bottom: 15px;

      }

      p {
        font-size: 14px;
        line-height: 1.5;
        font-weight: 300;
        color: #676767;
      }
    }
  }
}

.story-image-wrap {
  position: relative;
  z-index: 1;
  transform-origin: center;

  .story-text-wrap {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 0;
    overflow: hidden;

    h2 {
      color: #313131;
      font-size: 90px;
      font-weight: 900px;
      opacity: 0.2;
      transform-origin: center;
    }
  }

  .image {
    width: 100%;
    filter: drop-shadow(0px 0px 12px rgba(0, 0, 0, 0.25));
  }

}
</style>