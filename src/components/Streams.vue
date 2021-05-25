<template>
  <div class="cam-app">
    <small class="logout-btn" @click="logout">Log out</small>
    <br />
    <h4 class="d-flex pr-4 justify-content-end">Your cams</h4>

    <div v-if="show_camera > 0">
      <Camera :key="show_camera" :camera="selected_camera" />
      <small
        >{{ selected_camera.title }} ({{ selected_camera.description }})</small
      >
    </div>
    <img
      v-else
      src="https://static.tildacdn.com/tild3633-3263-4536-b865-663337613130/Artboard.svg"
    />
    <div class="cam-list" style="overflow: auto; max-height: 300px">
      <div
        class="cam-item"
        v-for="(camera, i) in camers"
        :key="i"
        @click="showCamera(camera)"
      >
        {{ camera.title }} <br />
        <small> {{ camera.description }} </small>
      </div>
    </div>
  </div>
</template>

<script>
import Camera from "./Camera.vue";
import axios from "axios";
export default {
  components: { Camera },
  data() {
    return {
      selected_camera: {},
      show_camera: 0,
      camers: [],
    };
  },
  mounted() {
    if (localStorage.token_session.length > 5) {
      axios
        .post("http://sova-back.ru")
        .then((response) => (this.camers = response.data))
        .then(() => (this.selected_camera = this.camers[0]));
    } else {
      this.$router.push({ name: "Login" });
    }
  },
  methods: {
    showCamera(camera) {
      this.selected_camera = camera;
      this.show_camera += 1;
    },
    logout() {
      this.logoutLink = false;
      axios
        .post(
          "http://sova-back.ru/logout",
          { token: localStorage.token_session },
          {
            headers: {
              "Content-Type": "application/json",
            },
          }
        )
        .then(() => {
          localStorage.token_session = "";
          this.$router.push({ name: "Login" });
        })
        .then((response) => {
          localStorage.token_session =
            response?.data !== undefined ? response.data : null;
        });
    },
  },
};
</script>

<style scoped>
@media (max-width: 1200px) {
  .cam-app {
    width: 95% !important;
    min-height: 100% !important;
  }
  .cam-item {
    height: 100% !important;
    padding: 7px !important;
  }
  .cam-list {
    max-height: 45vh !important;
    overflow: auto;
  }
  h4 {
    justify-content: flex-start !important;
  }
}
.cam-app {
  width: 600px;
  margin: auto;
  border-radius: 18px;
  padding-bottom: 30px;
  background: #fff;
}
.cam-item {
  cursor: pointer;
  border-bottom: 1px solid rgba(139, 138, 141, 0.2);
  font-size: 17px;
  height: 52px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  text-align: left;
  border-left: 3px solid rgba(255, 166, 0, 0);
  padding-left: 15px;
}
.cam-item:hover {
  transition: 1s;
  border-left: 3px solid rgb(255, 102, 0);
}
small {
  font-size: 12px;
  opacity: 0.5;
}
.logout-btn {
  opacity: 0.5;
  cursor: pointer;
}

::-webkit-scrollbar-button {
  background-image: url("");
  background-repeat: no-repeat;
  width: 5px;
  height: 0px;
  opacity: 0.5;
}

::-webkit-scrollbar-track {
  background-color: #ecedee;
}

::-webkit-scrollbar-thumb {
  -webkit-border-radius: 0px;
  border-radius: 0px;
  background-color: rgb(255, 136, 0);
}

::-webkit-scrollbar-thumb:hover {
  background-color: rgb(255, 136, 0);
}

::-webkit-resizer {
  background-image: url("");
  background-repeat: no-repeat;
  width: 4px;
  height: 0px;
}

::-webkit-scrollbar {
  width: 4px;
}
</style>
