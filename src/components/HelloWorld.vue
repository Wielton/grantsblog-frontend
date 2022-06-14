<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to Grant's Blog About Nothing
        </h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col
        class="mb-5"
        cols="4"
        
      >
      <v-card
        center>
        <v-text-field
          label="Username"
          v-model="userName"
          ></v-text-field>
        <v-textarea
          outlined
          style="width:85%"
          type="text"
          label="Post" 
          v-model="userPost"
          counter="200"></v-textarea>
          <v-card-actions>
            <v-btn @click="createPost">Create</v-btn>
          </v-card-actions>
      </v-card>
      </v-col>
        <!-- <v-row justify="center"> -->
          <v-col 
              class="mb-5"
              cols="6"
              >
              <v-btn @click="getPosts">See All</v-btn>
          <v-card
            v-for="post in posts"
            :key="post.id"
            :bind="post"
            style="background-color:#383838;border:1px solid white"
          >
            <v-card-title style="color:whitesmoke">{{post.username}}</v-card-title>
            <v-card-text style="color:whitesmoke">{{post.post}}</v-card-text>
            <v-card-actions>
              <v-btn @click="editPost" style="background-color:green">Edit</v-btn>
              <v-btn @click="deletePost" style="background-color:red">Delete</v-btn>
            </v-card-actions>
          </v-card>
          </v-col>
        <!-- </v-row> -->
      

      <v-col
        class="mb-5"
        cols="12"
      >
        
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'HelloWorld',

    data: () => ({
      userName: null,
      userPost: null,
      posts : []
    }),
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
        method : "UPDATE",
        data : {
          userPost : this.userPost
        }
    }).then((response)=>{
      this.posts = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
    deletePost(){
      axios.request({
        url : process.env.VUE_APP_API_URL+"posts",
        method : "DELETE"
    }).then((response)=>{
      this.posts = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
  },
  }
</script>
