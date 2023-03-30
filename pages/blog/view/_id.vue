<template>
    <div>
    <h1>{{ post.title }}</h1>
    <h2>{{ post.content }}</h2>
    <p>{{ post.tags }}</p>
    <p>{{ date(post.created_at) }}</p>
  </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        error: false,
        post: {}
      };
    },
    async mounted(){
        this.post = await this.getPost();
        console.log(this.post)
    },
    methods: {
      async getPost() {
        try{
          this.author_id = 2;
          const res = await this.$axios.get("/post/view/" + this.$route.params.id + "/");
          return res.data.data;
        }catch(e){
          console.error(e)
          this.error = true
        }
      },
      date(date){
        var d = new Date(date);
        return d.getDate()  + "-" + (d.getMonth()+1) + "-" + d.getFullYear() + " " + d.getHours() + ":" + d.getMinutes();
      }
    },
  };
  </script>