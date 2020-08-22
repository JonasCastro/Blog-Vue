<template>
    <div id="add-blog">
      <div id="form">
          <h2>Add a New Blog Post</h2>
          <form v-if="!submitted">
              <label>Blog Title:</label>
              <input type="text" v-model.lazy="blog.title" required />
              <label>Blog Content:</label>
              <textarea v-model.lazy.trim="blog.content"></textarea>
              <div id="checkboxes">
                  <p>Blog Categories:</p>
                  <label>Ninjas</label>
                  <input type="checkbox" value="ninjas" v-model="blog.categories" />
                  <label>Wizards</label>
                  <input type="checkbox" value="wizards" v-model="blog.categories" />
                  <label>Mario</label>
                  <input type="checkbox" value="mario" v-model="blog.categories" />
                  <label>Cheese</label>
                  <input type="checkbox" value="cheese" v-model="blog.categories" />
              </div>
              <label>Author:</label>
              <select v-model="blog.author">
                  <option v-for="author in authors">{{ author }}</option>
              </select>
              <hr />
              <button v-on:click.prevent="post">Add Blog</button>
          </form>
          <div v-if="submitted">
              <h3>Thanks for adding your post</h3>
          </div>
        </div>
        <div id="preview">
            <h3>Preview blog</h3>
            <p><strong>Blog title: </strong> {{ blog.title }}</p>
            <p><strong>Blog content:</strong></p>
            <p style="white-space: pre">{{ blog.content }}</p>
            <p><strong>Blog Categories:</strong></p>
            <ul>
                <li v-for="category in blog.categories">{{ category }}</li>
            </ul>
            <p><strong>Author:</strong> {{ blog.author }}</p>
        </div>
    </div>
</template>

<script>
// Imports
export default {
    data () {
        return {
            blog: {
                title: '',
                content: '',
                categories: [],
                author: ''
            },
            authors: ['The Net Ninja', 'The Angular Avenger', 'The Vue Vindicator'],
            submitted: false
        }
    },
    methods: {
        post: function(){
            this.$http.post('http://jsonplaceholder.typicode.com/posts', {
                title: this.blog.title,
                body: this.blog.content,
                userId: 1
            }).then(function(data){
                console.log(data);
                this.submitted = true;
            });
        }
    }
}
</script>

<style scoped>
#add-blog *{
    box-sizing: border-box;
}
#add-blog{
    display: flex;
    justify-items: center;
}
label{
    display: block;
    margin: 20px 0 10px;
}
input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
}
#form{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    width: 50%;
}
#preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    flex: 1;

}
h3{
    margin-top: 10px;
}
#checkboxes input{
    display: inline-block;
    margin-right: 10px;
}
#checkboxes label{
    display: inline-block;
    margin-top: 0;
}
button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
</style>
