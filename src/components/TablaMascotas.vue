<template>
    <div id="tabla-mascotas">
        <div v-if="!mascotas.length" class="alert alert-info" role="alert">
            No se han agregado mascotas
        </div>
        <table class="table">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <!-- <th>Apellido</th>
                    <th>Email</th> -->
                </tr>
            </thead>
            <tbody>
                <tr v-for="mascota in mascotas" :key="mascota.id">
                    <td v-if="editando === mascota.id">
                        <input type="text" class="form-control" v-model="mascota.nombre" />
                    </td>
                    <td v-else>
                        {{ mascota.nombre}}
                    </td>
                    <!-- <td v-if="editando === mascota.id">
                        <input type="text" class="form-control" v-model="mascota.apellido" />
                    </td> -->
                    <!-- <td v-else>
                        {{ mascota.apellido}}
                    </td>
                    <td v-if="editando === mascota.id">
                        <input type="email" class="form-control" v-model="mascota.email" />
                    </td>
                    <td v-else>
                        {{ mascota.email}}
                    </td> -->
                    <td v-if="editando === mascota.id">
                        <button class="btn btn-success" @click="guardarMascota(mascota)">💾 Guardar</button>
                        <button class="btn btn-secondary ml-2" @click="cancelarEdicion(mascota)">❌ Cancelar</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-info" @click="editarMascota(mascota)">✏️ Editar</button>
                        <button class="btn btn-danger ml-2" @click="$emit('delete-mascota', mascota.id)">🗑️
                            Eliminar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
  
<script>
export default {
    name: 'tabla-mascotas',
    props: {
        mascotas: Array,
    },
    data() {
        return {
            editando: null,
        }
    },
    methods: {
        editarMascota(mascota) {
            this.mascotaEditada = Object.assign({}, mascota);
            this.editando = mascota.id;
        },
        guardarMascota(mascota) {
            if (!mascota.nombre.length /* || !mascota.apellido.length || !mascota.email.length */) {
                return;
            }
            this.$emit('actualizar-mascota', mascota.id, mascota);
            this.editando = null;
        },
        cancelarEdicion(mascota) {
            Object.assign(mascota, this.mascotaEditada);
            this.editando = null;
        }
    }
}
</script>
  
<style scoped>

</style>