<template>
  <router-link :to="clickUrl">
    <div class="card m-2">
      <img :src="imageUrl" class="card-img-top" alt="..." />
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ bodyText }}</p>
        <button class="btn btn-success m-2" @click="onPlaySong">Play</button>
        <button class="btn btn-warning" @click="onPauseSong">Pause</button>
        <p>The Status: {{status}}</p>
      </div>
    </div>
  </router-link>
</template>

<script>
import { Eventbus } from "../main";
export default {
  name: "Card",
  props: ["item"],
  data() {
    return {
      id: this.item.id,
      title: this.item.title,
      bodyText: this.item.bodyText,
      imageUrl: this.item.imageUrl,
      clickUrl: `${this.item.clickUrl}?id=${this.item.id}`,
      clickText: this.item.clickText,
      status: ""
    };
  },
  methods: {
    onPlaySong(event) {
      event.preventDefault();
      event.stopPropagation();
      this.status = "Playing";
      Eventbus.$emit("playSong", {
        id: this.id,
        status: this.status,
        title: this.title
      });
    
    },
    onPauseSong() {
      event.preventDefault();
      event.stopPropagation();
      this.status = "Pause";
      Eventbus.$emit("pauseSong", {
        id: this.id,
        status: this.status,
        title: this.title
      });
     
    }
  }
};
</script>

<style scoped></style>
