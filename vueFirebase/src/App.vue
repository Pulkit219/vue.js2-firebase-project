<template>
  <div id="app" class="container">
      <div class="page-header">
         <h1>Vue.js 2 & Firebase </h1>
      </div>

      <div class="panel panel-default">

        <div class="panel-heading">
        <h3>books list</h3>
        </div>
        <div class="panel-body">
        
        </div>

      </div>
    
    <router-view></router-view>
  </div>
</template>

<script>
import Firebase from 'firebase'

let config = {
      apiKey: "AIzaSyAC6wRuUiAfR-Qd68jz-c4V2h6hmZ0WP8s",
      authDomain: "vuejs-firebase-fd8b1.firebaseapp.com",
      databaseURL: "https://vuejs-firebase-fd8b1.firebaseio.com",
      storageBucket: "vuejs-firebase-fd8b1.appspot.com",
      messagingSenderId: "364673894809"
  };

let app = Firebase.initializeApp(config);
let db = app.database();

let booksRef = db.ref('books');


export default {
  name: 'app',
  firebase: {
    books:booksRef
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
