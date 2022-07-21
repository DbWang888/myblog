<template>
  <div id="show-blogs">
    <h1>博客总览</h1>
    <div v-for="blog in blogs" class="single-blog">
      <router-link v-bind:to="'blog/' + blog.id">
        <h2 v-rainbow>{{ blog.title }}</h2>
      </router-link>
      <article>
        {{ blog.body | snippet }}
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: "show-blogs",
  data() {
    return {
      blogs: [],
    };
  },
  created() {
    this.$http
    //   .get("http://jsonplaceholder.typicode.com/posts")
      .get("http://localhost:8080/all_articles?page_size=10&page_id=1")
      .then(function (data) {
        this.blogs = data.body;
        console.log(this.blogs);
      });
  },
};
</script>

<style>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}

.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
  border: 1px dotted #aaa;
}

#show-blogs a{
    text-decoration: none;
}
</style>
