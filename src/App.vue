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
        <tabla-mascotas :mascotas="mascotas" @delete-mascota="eliminarMascota"
          @actualizar-mascota="actualizarMascota" />
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

      ],
    }
  },
  methods: {
    async getMascotas() {
      try {
        const respuesta = await fetch('http://localhost:5000/mascotas/', {
          //mode: 'no-cors',
          method: 'GET',
          headers: {
            'Content-type': 'application/json'
          }
        });
        this.mascotas = await respuesta.json();
        //console.log(this.mascotas)
      } catch (error) {
        console.log(error)
      }
    },
    async actualizarMascota(id, mascotaActualizada) {

      console.log(id, '-<> ', mascotaActualizada)

      try {
        const respuesta = await fetch(`http://localhost:5000/mascotas/${id}`, {
          //mode: 'no-cors',
          method: 'PUT',
          body: JSON.stringify(mascotaActualizada),
          headers: {
            'Content-type': 'application/json'
          }
        });
        this.mascotasModificada = await respuesta.json();
        this.mascotasModificada = this.mascotas.map((mascota) =>
          mascota.id === id ? mascotaActualizada : mascota
        )

      } catch (error) {
        console.log(error)
      }



    },
    async agregarMascota(mascota) {

      let id = 0;

      if (this.mascotas.length > 0) {
        id = this.mascotas[this.mascotas.length - 1].id + 1;
      }
      this.mascotas = [...this.mascotas, { ...mascota, id }];

      try {
        mascota.id = id
        const respuesta = await fetch('http://localhost:5000/mascotas/', {
          //mode: 'no-cors',
          method: 'POST',
          body: JSON.stringify(mascota),
          headers: {
            'Content-type': 'application/json'
          }
        });
        const mascotasCreada = await respuesta.json();
        console.log(mascotasCreada)

      } catch (error) {
        console.log(error)
      }


    },
    async eliminarMascota(id) {
      try {
        const respuesta = await fetch(`http://localhost:5000/mascotas/${id}`, {
          //mode: 'no-cors',
          method: 'DELETE',
          headers: {
            'Content-type': 'application/json'
          }
        });
        const respuestaBK = await respuesta.json();
        alert('se elimino correctamente', respuestaBK)
        this.mascotas = this.mascotas.filter(
          mascota => mascota.id !== id
        );

      } catch (error) {
        console.log(error)
      }


    },


  },
  mounted() {
    this.getMascotas();
  }
}
</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}
</style>