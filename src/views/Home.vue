<template>
  <div class="home">
    <div class="row">
      <div class="col-3" :key="index" v-for="(song, index) in songs">
        <Card :item="song" />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "../components/Card";
import { Eventbus } from "../main";
const songs = [
  {
    id: 0,
    title: "First Song",
    bodyText: "",
    imageUrl:
      "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAPFBMVEWsrKz///+pqanDw8O0tLT29vampqbAwMD5+fnz8/PU1NTs7Oy3t7fa2trJycnk5OTo6OjX19fOzs7f399TPbzUAAADPUlEQVR4nO3a23KDIBSFYcUj4iHG93/XRhEEQWd6UU2d/7vppNswrmzUNpAkAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD8ltCOy+UieoCp/b54obzR2mhViGySaZrWqsmDMxXJeyg+xWLok7CYN6r+FOWU3ZtRVKmWxU5DZDK1un2Mpra1ovdrIu+2N8rqzojnCZ3TnM+0dY4RufKKgz+q9IrjH6c4c5ZQvFJfvUUUudwVVWTQLX95SZqYk4Si259nWm/VfcBPCjOCyOugON4W8TihyILTTNPXWiyHSPFthlCRYnvXtXjSw7BL9rBwGjodFn2sqPbDX+Uw4dbCemomO+1eOuFkXsux2dqpm1jaFqqm2dp5VxMPE9p5+EpKUSbmplMvz01hEo+fB3rZ2kTLxWZf9nPRNnT6toRmkhb696Jwj8vNWZfeGOn80k7S91K0Ee+apocJ8zVSsyZsnJloZ/A68+y89I5cBzSPFZlfl8p1mLCtvd/bUHNi06ZiPWl7Wc6vzUNGmueD8g++GglJqIsk/P8Jh8cnzNZ/o5cXT0xovgnRf9E9MqE34uMSCsdy5NMSimawXo+805TuVx0kvAMJSUjC5P8nFJOUqn5ywqX4+P8tyscnfH4PSUjCP0VCEuoiCb864brJwq4ouQnrdYuK/dt0STiuRZNQfmlCc2JqTajc48wSYaNX1+yKobe6pj8b2/zbV9eq0pE4femW75jMroW1bSbSvAgq7Hr4MjHtiHW7LJ+ahcfbV0gLaRXzx72txqu+6reFa90Yu7I9ZFVjMqSjLprAdVdVnV0fj27YuTKhq5grkS0jqVmqj+7T0Jdhsi2RhmN+TUK5VN5HlcTdjeCY1ntLsJlo1t/UwpOE4Zao1NlQEemwOhvzdf+OoVingl5sjQjfVzhbwoIdNbftpjlPuN+cV7szTVR+F6W7O3M/w4fkPsd3mrmYuDcN5e/5Ebk7iyd/a2ZZuR/O+65rcNEOoc5WRTLqUy2GKriSymrSDwo55vuiENmgm6yacHvttUSEV07ytl1+Rt76+YQ+xegmYF3M40UAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8xA8fuyukzCBy3AAAAABJRU5ErkJggg==",
    clickUrl: "/song-detail",
    clickText: "Go to Detail",
    songStatus: ""
  },
  {
    id: 1,
    title: "Second Song",
    bodyText: "",
    imageUrl:
      "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAPFBMVEWsrKz///+pqanDw8O0tLT29vampqbAwMD5+fnz8/PU1NTs7Oy3t7fa2trJycnk5OTo6OjX19fOzs7f399TPbzUAAADPUlEQVR4nO3a23KDIBSFYcUj4iHG93/XRhEEQWd6UU2d/7vppNswrmzUNpAkAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD8ltCOy+UieoCp/b54obzR2mhViGySaZrWqsmDMxXJeyg+xWLok7CYN6r+FOWU3ZtRVKmWxU5DZDK1un2Mpra1ovdrIu+2N8rqzojnCZ3TnM+0dY4RufKKgz+q9IrjH6c4c5ZQvFJfvUUUudwVVWTQLX95SZqYk4Si259nWm/VfcBPCjOCyOugON4W8TihyILTTNPXWiyHSPFthlCRYnvXtXjSw7BL9rBwGjodFn2sqPbDX+Uw4dbCemomO+1eOuFkXsux2dqpm1jaFqqm2dp5VxMPE9p5+EpKUSbmplMvz01hEo+fB3rZ2kTLxWZf9nPRNnT6toRmkhb696Jwj8vNWZfeGOn80k7S91K0Ee+apocJ8zVSsyZsnJloZ/A68+y89I5cBzSPFZlfl8p1mLCtvd/bUHNi06ZiPWl7Wc6vzUNGmueD8g++GglJqIsk/P8Jh8cnzNZ/o5cXT0xovgnRf9E9MqE34uMSCsdy5NMSimawXo+805TuVx0kvAMJSUjC5P8nFJOUqn5ywqX4+P8tyscnfH4PSUjCP0VCEuoiCb864brJwq4ouQnrdYuK/dt0STiuRZNQfmlCc2JqTajc48wSYaNX1+yKobe6pj8b2/zbV9eq0pE4femW75jMroW1bSbSvAgq7Hr4MjHtiHW7LJ+ahcfbV0gLaRXzx72txqu+6reFa90Yu7I9ZFVjMqSjLprAdVdVnV0fj27YuTKhq5grkS0jqVmqj+7T0Jdhsi2RhmN+TUK5VN5HlcTdjeCY1ntLsJlo1t/UwpOE4Zao1NlQEemwOhvzdf+OoVingl5sjQjfVzhbwoIdNbftpjlPuN+cV7szTVR+F6W7O3M/w4fkPsd3mrmYuDcN5e/5Ebk7iyd/a2ZZuR/O+65rcNEOoc5WRTLqUy2GKriSymrSDwo55vuiENmgm6yacHvttUSEV07ytl1+Rt76+YQ+xegmYF3M40UAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8xA8fuyukzCBy3AAAAABJRU5ErkJggg==",
    clickUrl: "/song-detail",
    clickText: "Go to Detail",
    songStatus: ""
  },
  {
    id: 2,
    title: "Third Song",
    bodyText: "",
    imageUrl:
      "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAPFBMVEWsrKz///+pqanDw8O0tLT29vampqbAwMD5+fnz8/PU1NTs7Oy3t7fa2trJycnk5OTo6OjX19fOzs7f399TPbzUAAADPUlEQVR4nO3a23KDIBSFYcUj4iHG93/XRhEEQWd6UU2d/7vppNswrmzUNpAkAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD8ltCOy+UieoCp/b54obzR2mhViGySaZrWqsmDMxXJeyg+xWLok7CYN6r+FOWU3ZtRVKmWxU5DZDK1un2Mpra1ovdrIu+2N8rqzojnCZ3TnM+0dY4RufKKgz+q9IrjH6c4c5ZQvFJfvUUUudwVVWTQLX95SZqYk4Si259nWm/VfcBPCjOCyOugON4W8TihyILTTNPXWiyHSPFthlCRYnvXtXjSw7BL9rBwGjodFn2sqPbDX+Uw4dbCemomO+1eOuFkXsux2dqpm1jaFqqm2dp5VxMPE9p5+EpKUSbmplMvz01hEo+fB3rZ2kTLxWZf9nPRNnT6toRmkhb696Jwj8vNWZfeGOn80k7S91K0Ee+apocJ8zVSsyZsnJloZ/A68+y89I5cBzSPFZlfl8p1mLCtvd/bUHNi06ZiPWl7Wc6vzUNGmueD8g++GglJqIsk/P8Jh8cnzNZ/o5cXT0xovgnRf9E9MqE34uMSCsdy5NMSimawXo+805TuVx0kvAMJSUjC5P8nFJOUqn5ywqX4+P8tyscnfH4PSUjCP0VCEuoiCb864brJwq4ouQnrdYuK/dt0STiuRZNQfmlCc2JqTajc48wSYaNX1+yKobe6pj8b2/zbV9eq0pE4femW75jMroW1bSbSvAgq7Hr4MjHtiHW7LJ+ahcfbV0gLaRXzx72txqu+6reFa90Yu7I9ZFVjMqSjLprAdVdVnV0fj27YuTKhq5grkS0jqVmqj+7T0Jdhsi2RhmN+TUK5VN5HlcTdjeCY1ntLsJlo1t/UwpOE4Zao1NlQEemwOhvzdf+OoVingl5sjQjfVzhbwoIdNbftpjlPuN+cV7szTVR+F6W7O3M/w4fkPsd3mrmYuDcN5e/5Ebk7iyd/a2ZZuR/O+65rcNEOoc5WRTLqUy2GKriSymrSDwo55vuiENmgm6yacHvttUSEV07ytl1+Rt76+YQ+xegmYF3M40UAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8xA8fuyukzCBy3AAAAABJRU5ErkJggg==",
    clickUrl: "/song-detail",
    clickText: "Go to Detail",
    songStatus: ""
  }
];

export default {
  name: "Home",
  components: {
    Card
  },
  data() {
    return {
      songs
    };
  },

  created() {
    Eventbus.$on("playSong", data => {
      this.songs.forEach(song => {
        if (song.id === data.id) {
          song.songStatus = data.status;
        }
      });
    });
  }
};
</script>
