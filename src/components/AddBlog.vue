<template>
  <div class="AddBlog">
    <h2>添加博客</h2>
    <form v-show="!show">
      <label>博客标题:</label>
      <input v-model="blog.title">
      <label>博客内容:</label>
      <textarea v-model="blog.content"></textarea>
      <div id="chexbox">
        <label>vue.js</label>
        <input type="checkbox" v-model="blog.categories" value="vue.js">
        <label>node.js</label>
        <input type="checkbox" v-model="blog.categories" value="node.js">
        <label>java</label>
        <input type="checkbox" v-model="blog.categories" value="java">
      </div>
      <select v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button v-on:click.prevent="post">提交博客</button>
    </form>
    <h2 v-show="show">添加成功</h2>
    <hr>
    <div id="preview">
      <h2>博客总览</h2>
      <p>博客标题:{{blog.title}}</p>
      <p>博客内容:{{blog.content}}</p>
      <label>分类:</label>
      <ul>
        <li v-for="category in blog.categories">{{category}}</li>
      </ul>
      <p>作者:{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddBlog",
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
      },
      authors: ["cq", "xk", "xyc"],
      show:false
    };
  },
  methods: {
    post: function() {
      this.$http
        .post("http://jsonplaceholder.typicode.com/posts", {
          userId: 1,
          id: 1,
          title: this.blog.title,
          body: this.blog.content
        })
        .then(function(item) {
          console.log(item);
          this.show=true;
        });
    }
  }
};
</script>

<style>
</style>
