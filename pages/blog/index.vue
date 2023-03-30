<template>
  <div>
    <v-card
      class="mx-auto"
      width="45%"
      v-for="(post, index) in posts"
      :key="index"
      style="float: left; margin: 2% 2% !important;"
    >
      <v-img
        src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
        height="200px"
        cover
      ></v-img>

      <v-card-title> {{ post.title }} </v-card-title>
      <p style="margin-left: 15px;"> {{ post.content }} </p>
      <v-card-subtitle style="margin-left: 15px; font-size: 12px;"> {{ post.tags }} </v-card-subtitle>

      <v-card-actions>
        <NuxtLink :to="'/blog/view/' + post.id + '/'">
          <v-btn color="orange-lighten-2" variant="text"> Read </v-btn>
        </NuxtLink>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
    };
  },
  async mounted() {
    this.posts = await this.getBlogs();
  },
  methods: {
    async getBlogs() {
      const res = await this.$axios.get("/post/allposts/");
      return res.data.data;
    },
  },
};
</script>