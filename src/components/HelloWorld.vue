<template>
  <div>
      <v-btn color="primary" @click="getPosition()">
          Get Position
      </v-btn>
      <div v-if="geolocation.latitude">
        You are located at: {{geolocation.latitude}}, {{geolocation.longitude}}
      </div>

      <div v-else-if="loadingPosition">
        Acquiring your position
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loadingPosition: false,
      geolocation: {}
    }
  },
  created() {
    window.addEventListener("deviceready", this.onDeviceReady, false);
  },
  methods: {
    onDeviceReady() {
      console.log("navigator.geolocation works well");
    },
    getPosition() {
      this.loadingPosition = true;

      navigator.geolocation.getCurrentPosition(({ coords }) => {
        this.loadingPosition = false;
        this.geolocation = coords;
      });
    }
  }
}
</script>