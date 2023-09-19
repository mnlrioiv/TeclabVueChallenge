<template>
    
    <div class="reservation-form">
    <h2>Reservar</h2>
      <div class="form-row">
        <div class="form-group">
          <label for="name">Nombre:</label>
          <input v-model="name" type="text" id="name" />
        </div>
        <div class="form-group">
          <label for="date">Fecha:</label>
          <input v-model="date" type="date" id="date" />
        </div>
        <div class="form-group">
          <label for="time-from">Desde:</label>
          <input v-model="timeFrom" type="time" id="time-from" />
        </div>
        <div class="form-group">
          <label for="time-to">Hasta:</label>
          <input v-model="timeTo" type="time" id="time-to" />
        </div>
        <button @click="addReservation">Guardar</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        date: '',
        timeFrom: '',
        timeTo: ''
      };
    },
    methods: {
      addReservation() {
        // Valido que la hora este ok
        if (this.timeFrom >= this.timeTo) {
          alert('La hora Hasta no puede ser menor o igual a la hora Desde');
          return;
        }
  
        const reservation = {
          name: this.name,
          date: this.date,
          timeFrom: this.timeFrom,
          timeTo: this.timeTo
        };
  
        this.$emit('add-reservation', reservation);
  
        //Luego de reservar blanqueo los campos
        this.name = '';
        this.date = '';
        this.timeFrom = '';
        this.timeTo = '';
      }
    }
  };

  
  </script>
  
<style scoped>
.reservation-form .form-row {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
</style>