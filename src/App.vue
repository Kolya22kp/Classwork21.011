<template>
  <v-app id="app">
    <v-navigation-drawer
      color="green"
      dark
      expand-on-hover
      hide-overlay
      permanent
      location="right"
      absolute
      app
    >
      <v-list-item two line
          nav
          shaped
          dense
      >
        <v-list-item-avatar>
          <img :src="`avatar`" alt="">
        </v-list-item-avatar>

        <v-list-item-content class="text-left">
          <v-list-item-title class="font-weight-black">{{ name }}</v-list-item-title>
          <v-list-item-subtitle>{{ subname }}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider class="my-3"></v-divider>
      <v-list-item link :to="/user">
        <v-list-item-icon>
          <v-icon>mdi-home-outline</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title class="text-left">Главная</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-navigation-drawer>

    <v-main class="px-12 py-3">
      <v-container fluid>
        <div>
          <v-row class="text-left">
            <v-col cols="10">
              <h1 class="green--text text--darken-2">
                <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                Иван Иванов
              </h1>
            </v-col>
          </v-row>
          <v-row class="text-left">
            <v-col cols="2">
              <img src="https://randomuser.me/api/portraits/men/7.jpg" style="max-width: 100%" alt="">
            </v-col>
            <v-col cols="10" class="text-left">
              <p>
                Веб-сайт: <a href="#" target="_blank">...</a>
              </p>
              <p>
                E-mail: <a href="mailto:...">...</a>
              </p>
              <p>
                Город: ...
              </p>
              <p>
                Место работы: ...
              </p>
            </v-col>
          </v-row>

          ОСТАЛЬНОЕ СОДЕРЖИМОЕ СТРАНИЦЫ
        </div>
        <v-card>
          <router-view/>
        </v-card>
      </v-container>
    </v-main>

  </v-app>
</template>

<script>
import homeView from "@/views/HomeView.vue";
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  computed: {
    HelloWorld() {
      return HelloWorld
    },
    homeView() {
      return homeView
    }
  },
  data: () => {
    return {
      avatar: '',
      name: '',
      subname: ''
    }
  },
  methods: {
    getUserData() {
      this.axios({
        method: 'get', // метод GET для получения данных с API
        url: 'https://randomuser.me/api/', // адрес API
      }).then((response) => {
        // парсинг результата ответа от сервера
        console.log(response.data);
        this.name = response.data.results[0].name.first;
        this.subname = response.data.results[0].name.last;
        this.avatar = response.data.results[0].picture.medium;
      })
    }
  },
  mounted() {
    // хук для первичной загрузки метода
    this.getUserData();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
