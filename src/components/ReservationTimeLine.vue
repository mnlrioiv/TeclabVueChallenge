<template>
    <div class="reservation-timeline">
      <vue-timeline
        :items="timelineItems"
        :column-width="200"
        :min-width="600"
      ></vue-timeline>
    </div>
  </template>
  
  <script>
  import VueTimeline from 'vue-timeline-component';
  
  export default {
    components: {
      VueTimeline
    },
    props: {
      timelineItems: Array
    }
  };
  </script>
  
  