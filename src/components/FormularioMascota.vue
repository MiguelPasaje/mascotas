<template>
    <div id="formulario-mascota">
        <form @submit.prevent="enviarFormulario">
            <div class="container">
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Nombre</label>
                            <input v-model="mascota.nombre" type="text" class="form-control" />
                        </div>
                    </div>
                    <!--<div class="col-md-4">
                        <div class="form-group">
                            <label>Apellido</label>
                            <input v-model="mascota.apellido" type="text" class="form-control" />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Email</label>
                            <input v-model="mascota.email" type="email" class="form-control" />
                        </div>
                    </div> -->
                </div>
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <button class="btn btn-primary">Añadir mascota</button>
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>
  
<script>
export default {
    name: 'formulario-mascota',
    data() {
        return {
            mascota: {
                nombre: '',
                /*  apellido: '',
                 email: '', */
            },
        }
    },
    methods: {
        enviarFormulario() {
            this.$emit('add-mascota', this.mascota);
        }
    }
}
</script>
  
<style scoped>
form {
    margin-bottom: 2rem;
}
</style>