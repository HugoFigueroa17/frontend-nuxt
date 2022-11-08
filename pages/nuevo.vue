<style scoped>
        @import '~/static/css/index.css';
</style>
<template>

    <div>
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
                <h2 class="text-center">Nuevo usuario</h2>
                </div>
                <div class="card-body">
                    <form v-on:submit.prevent="guardarUsuario()">
                        <div class="row">
                            <div class="col-12">
                                <label>Nombre completo</label>
                                <input type="text" class="form-control" v-model="user.fullname" required/>
                            </div>
                        </div>
                        <div class="row mt-2">
                            <div class="col-6">
                                <label>e-mail</label>
                                <input type="email" class="form-control" v-model="user.email" required/>
                            </div>
                            <div class="col-6">
                                <label>Teléfono</label>
                                <input type="text" class="form-control" v-model="user.phone" maxlength="10"  v-mask="'###-###-##-##'" required/>
                            </div>
                        </div>
                        <div class="row mt-2">
                            <div class="col-6">
                                <label>Username</label>
                                <input type="text" class="form-control" v-model="user.username" required/>
                            </div>
                            <div class="col-6">
                                <label>Contraseña</label>
                                <input type="password" class="form-control" v-model="user.password" minlength="8" required/>
                            </div>
                        </div>
                        <div class="row mt-3">
                            <div class="col-md-12">
                                <label>Edad</label>
                                <input type="number" class="form-control" v-model="user.age" min="0" max="100" required/>
                            </div>
                        </div>
                        <div class="row justify-content-center mt-2">
                            <div class="col-md-3">
                                <button type="submit" class="btn btn-success btn-block">Guardar</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
            </div>
        </div> 
        </div>
    </div>
</template>

<script>
export default {
    
    data(){
        return {
                user: {
                fullname:'',
                email:'',
                phone:'',
                username:'',
                password:'',
                age:''
            }
        }
    },
    methods:{
        async guardarUsuario(){
            try{
                const response = await this.$axios.post("users",this.user);
                const data = response.data;

                if(data.id){
                    this.$swal('¡El usuario se creo exitosamente!').then((result) => {
                        this.$router.push('/');
                    });
                }
                else
                {
                    this.$swal(data.response);
                }
            }catch(e){

            }finally{

            }
        }
    }
}
</script>