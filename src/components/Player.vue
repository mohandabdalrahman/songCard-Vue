<template>
  <div class="player p-3 d-flex justify-content-around">
    <p>Current song: {{ title }}</p>
    <p>with ID: {{ id }}</p>
    <p>status : {{status}}</p>
  </div>
</template>

<script>
import { Eventbus } from "../main";

export default {
  data() {
    return {
      title: "",
      id: "",
      status: ""
    };
  },
  created() {
    Eventbus.$on("playSong", data => {
      this.title = data.title;
      this.id = data.id;
      this.status = data.status;
    });

    Eventbus.$on("pauseSong", data => {
      this.title = data.title;
      this.id = data.id;
      this.status = data.status;
    });
  }
};
</script>

<style scoped>
.player {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>
