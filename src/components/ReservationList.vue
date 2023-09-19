<template>
    <div class="reservation-list">
      <h2>Agenda de reservas</h2>
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Fecha</th>
            <th>Desde</th>
            <th>Hasta</th>
            <th>Acción</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(reservation, index) in reservations" :key="index">
            <td>{{ reservation.name }}</td>
            <td>{{ reservation.date }}</td>
            <td>{{ reservation.timeFrom }}</td>
            <td>{{ reservation.timeTo }}</td>
            <td><button @click="deleteReservation(index)">Eliminar reserva</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      reservations: Array
    },
    methods: {
      deleteReservation(index) {
        this.$emit('delete-reservation', index);
      }
    }
  };
  </script>
  
  