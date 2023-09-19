<template>
  <div id="app">
    <reservation-form @add-reservation="addReservation" />
    <reservation-timeline :timeline-items="reservations" />
    <reservation-list
      :reservations="reservations"
      @delete-reservation="deleteReservation"
    />
    <vue-timeline :data="reservations"></vue-timeline>
  </div>
</template>

<script>
import ReservationForm from './components/ReservationForm.vue';
import ReservationList from './components/ReservationList.vue';
import ReservationTimeline from './components/ReservationTimeLine.vue';
import moment from 'moment';
import VueTimeline from "vue-timeline-component"

export default {
  components: {
    ReservationForm,
    ReservationList,
    ReservationTimeline,
    VueTimeline
  },
  data() {
    return {
      reservations: [],
      timelineItems: [],
    };
  },
  methods: {
    addReservation(reservation) {
      // Valida la hora
      if (moment(reservation.timeTo, 'HH:mm') <= moment(reservation.timeFrom, 'HH:mm')) {
        alert('La fecha desde debe ser menor a la fecha hasta');
        return;
      }

      this.reservations.push(reservation);

      // Formateo fechas y horas para mostrar
      const formattedReservation = {
        name: reservation.name,
        start: moment(reservation.date + ' ' + reservation.timeFrom).format('YYYY-MM-DD HH:mm:ss'),
        end: moment(reservation.date + ' ' + reservation.timeTo).format('YYYY-MM-DD HH:mm:ss')
      };

      this.timelineItems.push(formattedReservation);
    },
    deleteReservation(index) {
      this.reservations.splice(index, 1);
      this.timelineItems.splice(index, 1);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

h2 {
  margin-bottom: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

button {
  background-color: #0b8a35;
  color: white;
  border: none;
  padding: 6px 12px;
  cursor: pointer;
}

button:hover {
  background-color: #04430a;
}

</style>
