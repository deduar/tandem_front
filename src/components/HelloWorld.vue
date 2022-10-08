<template>
  <div>
    <ul>
      <div class="card_menu">
        <li><button><a href=".">Get Twitts</a></button></li>
        <li><button><a href="/stored">Twits Stored</a></button></li>
        <li><button><a href="/delete">Delete All Twits</a></button></li>
        <li><button><a href="/graphs">Show Graphs</a></button></li>    
      </div>
    </ul>
    <ul v-if="posts && posts.length">
      <li v-for="post of posts" v-bind:key="post.id">
        <div class="card" style="margin: 20px; background: #f5f5f5">
          <div class="container" style="padding: 10px">
            {{ post.id }}
            <div class="card_head">
              <img v-bind:src="post.user.profile_image_url" />
              <h4>{{ post.user.name }}</h4>
            </div>
            <strong>{{ post.text }}</strong>
            <p style="display: flex; justify-content: space-between;">
              Índice 1:{{ post.entities.hashtags[0].indices[0] }} " | " 
              Índice 2:{{ post.entities.hashtags[0].indices[1] }}
              <button><a v-bind:href="'/save/'+ post.id">Save</a></button>
            </p>
            
          </div>
        </div>
      </li>
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="error of errors" v-bind:key="error.id">
        {{ error.message }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      posts: [],
      errors: [],
    };
  },

  // Fetches posts when the component is created.
  async created() {
    await axios
      .get(`http://localhost:8000/api/tw`)
      .then((response) => {
        // JSON responses are automatically parsed.
        this.posts = response.data.data.statuses;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  /* display: inline-block; */
  margin: 0 10px;
}
a {
  color: #42b983;
}

.card {
  /* Add shadows to create the "card" effect */
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: 90%;
}

/* On mouse-over, add a deeper shadow */
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

/* Add some padding inside the card container */
.container {
  padding: 2px 16px;
}

.card_head {
  display: flex;
  align-items: stretch;
  margin-bottom: 8px;
}

.card_menu {
  display: flex;
  /* align-items: center; */
  justify-content: center;
}

a {
  text-decoration: none
}
</style>
