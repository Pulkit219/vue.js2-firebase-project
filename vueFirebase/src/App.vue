<template>
  <div id="app" class="container">
      <div class="page-header">
         <h1>Vue.js 2 & Firebase </h1>
      </div>

      <div class="panel panel-default">

       <div class="panel-heading">
        <h3>Add book</h3>
        </div>
        <div class="panel-body">
            <form id="form" class="form-inline" v-on:submit.prevent ="addBook">
              <div class="form group">
              <label for="bookTitle">Title:</label><br/>
              <input type="text" id="bookTitle" class="form-control"  v-model="newBook.title">
              </div>

              <div class="form group">
              <label for="bookAuthor">Author:</label><br/>
              <input type="text" id="bookAuthor" class="form-control"  v-model="newBook.author">
              </div>

              <div class="form group">
              <label for="bookUrl">Url:</label><br/>
              <input type="text" id="bookUrl" class="form-control"  v-model="newBook.url">
              </div><br/>
              <input type="submit" value="add book" class="btn btn-primary">
            </form>
        </div>
        </div>




       <div class="panel panel-default">
        <div class="panel-heading">
        <h3>books list</h3>
        </div>
        <div class="panel-body">
              <table class="table table-striped">
                <thead>
                  <tr>
                    <th>Title</th> <th>author</th> 
                  </tr>
                </thead>
                <tbody>
                    <tr v-for="book in books">
                        <td><a v-bind:href="book.url">{{book.title}}</a></td>
                        <td>{{book.author}}</td>
                        <td><span class="glyphicon glyphicon-trash" v-on:click="removeBook(book)"> </span></td>
                    </tr>

                </tbody>
              </table>
        </div>

      </div>
    
   
  </div>
</template>

<script>
import Firebase from 'firebase'
import toastr from 'toastr'

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
  },
  data(){
    return{
        newBook: {
          title:'',
          author:'',
          url:''
        }
      
    }

  },
  methods:{
     addBook:function(){
       booksRef.push(this.newBook);
       this.newBook.title = '';
       this.newBook.author='';
       this.newBook.url='';
     },
     removeBook: function(book){
      
       booksRef.child(book['.key']).remove();
       toastr.success("book removed");
     }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}


.form-control{
  
  width:100%;
}

.form group input[type=text]{
   width:100%;
}

#bookUrl ,#bookAuthor ,#bookTitle {
    width: 100%;
    }
</style>
