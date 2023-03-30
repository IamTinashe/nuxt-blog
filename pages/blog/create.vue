<template>
  <div>
  <form v-if="success==false">
    <v-text-field
      v-model="title"
      :counter="100"
      label="Title"
      required
    ></v-text-field>

    <v-text-field
      v-model="content"
      label="Content"
      required
    ></v-text-field>

    <v-text-field
      v-model="tags"
      label="Tags"
      required
    ></v-text-field>

    <v-btn
      class="me-4"
      @click="submit()"
    >
      submit
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
  </form>
  <p v-if="success==true">Submitted Successfully <br> {{ data }}</p>
</div>
</template>

<script>
export default {
  data() {
    return {
      author_id: '',
      title: '',
      content: '',
      tags: '',
      error: false,
      succes: false,
      data: {}
    };
  },
  methods: {
    async submit() {
      try{
        this.author_id = 2;
        const res = await this.$axios.post("/post/add/", { author_id: this.author_id, title: this.title, content: this.content, tags: this.tags});
        this.success = true    
        this.data = res.data;
      }catch(e){
        console.error(e)
        this.error = true
      }
    },
  },
};
</script>