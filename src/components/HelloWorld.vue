<template>
  <div class="hello">
    <h1>Welcome to Grant's Blog About Nothing</h1>
    
      <input type="text" placeholder="Username" v-model="userName">
      <textarea type="text" placeholder="Post" v-model="userPost"></textarea>
      <button @click="createPost">CREATE</button>
      <button @click="getPosts">GET</button>
      <ul 
      v-for="post in posts"
      :key="post.id"
      :bind="post"
      >
        <li>{{post.username}}{{post.post}}</li>
      </ul>
  </div>   
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      userName : null,
      userPost : null,
      posts : []
    }
  },
  methods: {
    createPost(){
      axios.request({
        url : process.env.VUE_APP_API_URL+"posts",
        method : "POST",
        data : {
          userName : this.userName,
          userPost : this.userPost
        }
    }).then((response)=>{
      console.log(response)
      }).catch((error)=>{
        console.log(error)
      })
    },
    getPosts(){
      axios.request({
        url : process.env.VUE_APP_API_URL+"posts",
        method : "GET"
    }).then((response)=>{
      this.posts = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
    editPost(){
      axios.request({
        url : process.env.VUE_APP_API_URL+"posts",
        method : "GET"
    }).then((response)=>{
      this.postsArr = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
    deletePost(){
      axios.request({
        url : process.env.VUE_APP_API_URL+"posts",
        method : "GET"
    }).then((response)=>{
      this.postsArr = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
