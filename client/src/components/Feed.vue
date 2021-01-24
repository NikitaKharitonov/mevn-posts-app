<template>
  <div class="container">
    <div class="inputArea">
      <textarea class="textarea"
                @input="mixin_autoResize_resize" placeholder="What's new?" v-model="currentMessage"
                @focusin="setFocus(true);mixin_autoResize_resize"
                @focusout="setFocus(false)">
      </textarea>
      <button value="Post"
              v-if="isFocus || currentMessage.trim().length > 0"
      @click="createPost">Post
      </button>
    </div>
    <Post v-for="post in posts" v-bind:key="post._id" v-bind:text="post.text" v-bind:date="post.createdAt" v-on:dblclick="deletePost(post._id)" />

  </div>

</template>

<script>
import PostService from "../PostService";
import Post from "./Post"

export default {
  name: "Feed",
  data() {
    return {
      currentMessage: "",
      msg: "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur assumenda commodi, dicta dolore expedita explicabo ipsum libero maiores necessitatibus quo, sunt tempora totam unde vitae voluptatem. Libero nostrum quo voluptas!\n",
      isFocus: false,
      date: new Date(),
      posts: [],
      error: ""
    }
  },
  async created() {
    try {
      this.posts = await PostService.getPosts();
    } catch (err) {
      this.error = err.message;
    }
  },
  methods: {
    setFocus(isFocus) {
      this.isFocus = isFocus
    },
    mixin_autoResize_resize(event) {
      event.target.style.height = "auto";
      event.target.style.height = `${event.target.scrollHeight}px`;
    },
    async createPost() {
      await PostService.insertPost(this.currentMessage);
      this.posts = await PostService.getPosts();  
      // this.posts.unshift({
      //   id: this.posts.length, text: this.currentMessage, date: new Date()
      // })
      this.currentMessage = ""
    },
    async deletePost(id) {
      await PostService.deletePost(id);
      this.posts = await PostService.getPosts();
    }
  },
  // mounted() {
  //   this.posts = [
  //     {id: 1, text: this.msg, date: this.date},
  //     {id: 2, text: this.msg, date: this.date},
  //     {id: 3, text: this.msg, date: this.date},
  //   ]
  // },
  components: {
    Post
  }
}
</script>

<style scoped>

.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 60%;
  margin: auto;
  font-family: Arial, Helvetica, sans-serif;
}

.inputArea {
  background: #333336;
  border-radius: 4px;
  padding: 10px;
  height: auto;
  margin-bottom: 8px;

}

textarea {
  background: #333336;
  border: none;
  resize: none;
  color: white;
  width: 100%;
  box-sizing: border-box;
  outline: none;
  font-family: Arial, Helvetica, sans-serif;
}

button {
  color: white;
  background: #686868;
  border-radius: 4px;
  border: none;
  padding: 4px 8px;
  float: right;
}

.post {
  background: #333336;
  border-radius: 4px;
  padding: 10px;
  height: fit-content;
  margin-bottom: 8px;
}

.date {
  color: darkgrey;

}

@media screen and (max-width: 800px){
  .container{
    width: 100%;
  }
}

</style>