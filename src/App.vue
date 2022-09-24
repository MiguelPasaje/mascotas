<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Mascotas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <formulario-mascota @add-mascota="agregarMascota" />
        <tabla-mascotas :mascotas="mascotas" @delete-mascota="eliminarMascota" />
      </div>
    </div>
  </div>
</template>

<script>
import TablaMascotas from '@/components/TablaMascotas.vue'
import FormularioMascota from './components/FormularioMascota.vue'

export default {
  name: 'app',
  components: {
    TablaMascotas,
    FormularioMascota
  },
  data() {
    return {
      mascotas: [
        {
          id: 1,
          nombre: 'Jhon',
          /*  apellido: 'castillo',
           email: 'jhon@email.com', */
        },
        {
          id: 2,
          nombre: 'Taison',
          /*  apellido: 'tyr',
           email: 'taison@email.com', */
        },
        {
          id: 3,
          nombre: 'Dennis',
          /*   apellido: 'Targaryen',
            email: 'dennis@email.com', */
        },
      ],
    }
  },
  methods: {
    agregarMascota(mascota) {
      let id = 0;

      if (this.mascotas.length > 0) {
        id = this.mascotas[this.mascotas.length - 1].id + 1;
      }

      this.mascotas = [...this.mascotas, { ...mascota, id }];
    },
    eliminarMascota(id) {
      this.mascotas = this.mascotas.filter(
        mascota => mascota.id !== id
      );
    },


  }
}
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}
</style>