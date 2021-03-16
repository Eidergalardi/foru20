<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-primary">
      <a href="/" class="navbar-brand">Teacher's Forum Community FORÜ</a>
    </nav>
    <div class="container">
      <div class="row mt-5">
        <div class="col-sm-4">
          <div class="card">
            <div class="card-header">
              <h3>Crea un nuevo foro</h3>
            </div>
            <div class="card-body">
              <form @submit.prevent="addForums">
                <div class="form-group">
                  <label>
                    <input type="text" class="font-control" v-model="newForum.name" placeholder="Name">
                  </label>
                  <label>
                    <input type="text" class="font-control" v-model="newForum.author" placeholder="Author">
                  </label>
                  <label>
                    <input type="text" class="font-control" v-model="newForum.url" placeholder="Url">
                  </label>

                  <br><br>
                  <button type="submit" class="btn btn-primary">
                    Save
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="col-sm-8 text-center">
          <img src="./assets/logo.png" alt="">
          <div class="card">
            <div class="card-header">
              <h3>Lista de Foros</h3>
            </div>
            <div class="card-body">
              <table class="table table-striped table-bordered">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Autor</th>
                    <th>Message</th>
                  </tr>
                </thead>
                <tbody>

                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
//modulo para conectar a bd real
import Firebase from 'firebase';
import config from './config';

//app contiene conexion de firebase
let app = Firebase.initializeApp(config);

//db contiene conexion para usar el servicio
let db = app.database();
let forumsRef = db.ref('forums');
//let authentication = app.auth();

export default {
  name: 'App',
  firebase: {
    forums: forumsRef,
  },
  data(){
    return {
      newForum: {
        name: '',
        author: '',
        url: '',
      }
    }

  },
  methods:{
    addForums(){
      //console.log(this.newForum);
      forumsRef.push(this.newForum);
      this.newForum.name='';
      this.newForum.author='';
      this.newForum.url='';

    }
  }

}
</script>

<style>

#app {

}
</style>
