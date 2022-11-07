<template>
  <div>
    <Loader :isLoading="load"></Loader>
    <div class="navbar navbar-expand-lg navbar-dark bg-primary">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Users API</a>
      </div>
    </div>
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div class="card mt-4">
            <div class="card-header">
              <div class="text-right">
                <nuxt-link class="btn btn-success my-2 my-sm-0" to="nuevo">Agregar</nuxt-link>
              </div>
            </div>
            <div class="card-body">
              <table class="table table-hover">
               <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Nombre</th>
                  <th scope="col">e-mail</th>
                  <th scope="col">Teléfono</th>
                </tr>
                <tr>
                  <td v-if="users.length === 0"  colspan="4" class="text-center">No hay datos disponibles</td>
                </tr>
                <tr v-for="(m,i) in users" v-bind:key="i">
                  <td>{{i+1}}</td>
                  <td>{{m.fullname}}</td>
                  <td>{{m.email}}</td>
                  <td>{{m.phone}}</td>
                </tr>
               </thead> 

              </table>
            </div>
          </div>
        </div>
      </div> 
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data(){
    return {
      users: [],
      load: true
    }
  },
  methods:{
    async getUsers(path: string){
      const response = await this.$axios.get(path);
      return response.data;
    }
  },
  mounted(){
    this.$nextTick(async()=>{

      try{
        await Promise.all([this.getUsers('users')]).
        then((val) =>{
          this.users = val[0];
        });
      }catch(e){
        console.log(e)
      }finally{
        this.load = false;
      }
    })
  }
})
</script>
