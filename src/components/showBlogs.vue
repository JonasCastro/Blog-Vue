<template>
    <div id="show-blogs">
        <h1>All Blog Articles</h1>
        <input type="text" v-model="search" placeholder="Search Blogs" />
        <div class="list-blog">
          <div v-for="blog in filteredBlogs" class="single-blog">
              <router-link v-bind:to="'/blog/' + blog.id"><h2>{{ blog.title }}</h2></router-link>
              <article>{{ blog.body }}</article>
          </div>
        </div>
    </div>
</template>

<script>
// Imports
import searchMixin from '../mixins/searchMixin';
export default {
    data () {
        return {
            blogs: [],
            search: ''
        }
    },
    created() {
        this.$http.get('http://jsonplaceholder.typicode.com/posts').then(function(data){
            this.blogs = data.body.slice(0,10);
        });
    },
    mixins: [searchMixin]
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0px auto;
}
.list-blog{
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-gap: 20px;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;

  border-radius: 5px;
  transition: all 0.3s ease 0s;
}
.single-blog:hover{
     transform: translateY(-4px);
  }

#show-blogs a{
    color: #444;
    text-decoration: none;
}
 input {
   width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  }
</style>
