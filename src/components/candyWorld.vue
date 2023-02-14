<template>
  <v-container>
      <h1>Welcome to the World of Candies!</h1>
    <div>
      <div class="posts">
        <v-btn @click="getCandy">Candies</v-btn>
        <div v-for="candy in candies" :key="candy.candyTitle">
          <h4>Title: {{ candy.candyTitle }} {{ candy.candyBody }}</h4>
        </div>
      </div>
      <v-container>
        <div class="posts">
          <v-btn @click="addCandy">Post Candies</v-btn>
          <v-col>
            <v-text-field v-model="candyTitle" type="text"></v-text-field>
          </v-col>
          <v-text-field v-model="candyBody" type="text"></v-text-field>
        </div>
      </v-container>
      <v-container>
        <div class="posts">
          <v-btn @click="editCandy">Edit Candies</v-btn>
          <v-text-field v-model="candyTitle" type="text"></v-text-field>
          <v-text-field v-model="candyBody" type="text"></v-text-field>
        </div>
      </v-container>
      <v-container>
        <div class="posts">
          <v-btn @click="deleteCandy">Delete Candies</v-btn>
          <v-text-field v-model="candyTitle" type="text"></v-text-field>
        </div>
      </v-container>
    </div>
  </v-container>
</template>

<script>
import axios from 'axios';
  export default {
    name: 'candyWorld',
    props: {
      "title" : String,
      "body" : String,
    },
    data() {
      return {
        // apiUrl: process.env.VUE_APP_BASE_DOMAIN,
        candies: [],
        candyTitle: "",
        candyBody: "",
      }
    },
    methods: {
      getCandy() {
        axios.request({
          url: '${process.env.VUE_APP_BASE_DOMAIN}/api/candy',
          method: 'GET'
        }).then((response)=>{
          this.candy = response.data;
          console.log(response);
        }).catch((error)=>{
          error = "Something failed!"
          console.log(error);
        })
      },
      addCandy() {
        axios.request({
          url: this.apiUrl+'/api/candy',
          method: 'POST',
          data: {
            title: this.title,
            body: this.body
          }
        }).then((response)=>{
          this.candy = response.data;
          console.log(response);
        }).catch((error)=>{
          error = "Something failed adding!"
          console.log(error);
        })
      },
      editCandy() {
        axios.request({
          url: this.apiUrl+'/api/candy',
          method: 'PATCH',
          data: {
            title: this.title,
            body: this.body
          }
        }).then((response)=>{
          this.candy = response.data;
          console.log(response);
        }).catch((error)=>{
          error = "Something failed editing!"
          console.log(error);
        })
      },
      deleteCandy() {
        axios.request({
          url: this.apiUrl+'/api/candy',
          method: 'delete',
          data: {
            title : this.name
          }
        }).then((response)=>{
          this.candy = response.data;
          console.log(response);
        }).catch((error)=>{
          error = "Something failed deleting!"
          console.log(error);
        })
      }
    },
    mounted () {
      this.getCandy();
    },
  }
</script>

<style scoped>
.posts{
  margin-top: 10px;
  margin-left: 5px;
}
div{
  padding: 5px;
}
</style>