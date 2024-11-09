<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Component - Vue.js</title>
<link href="https://fonts.googleapis.com/css?family=Quicksand&display=swap" rel="stylesheet">
<style>
body {
  margin: 5%;
  font-family: 'Quicksand', sans-serif;
}
</style>
</head>
<body>
<div id="app">
  <header>
    <h1>What is Vue.js?</h1>
    <p>The Progressive JavaScript Framework!!</p>
  </header>
  <hr>
  <!-- deklarasi Dom Vue -->
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/kelas">Kelas</router-link>
  </nav>
  <main>
    <router-view></router-view>
  </main>
  <hr>
  <footer>
    <p>Praktisi Mengajar - 2024 | Vue.js</p>
  </footer>
</div>
<!-- include Vue.js dan Vue Router Snippet -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
<script src="https://cdn.jsdelivr.net/npm/vue-router@3"></script>
<script>
const Home = {
  template: '<div><h2>Home Page</h2><p>Welcome to the Home page!</p></div>'
};

const About = {
  template: '<div><h2>About Page</h2><p>About Vue.js and this simple application.</p></div>'
};

const Kelas = {
  template: `
    <div>
      <h3>Tambah Kelas</h3>
      <p><input type="text" placeholder="Nama Kelas" v-on:keyup.enter="tambahKelas" v-model="kelasBaru"></p>
      <hr>
      <h3>Daftar Kelas - ({{ dataKelas.length }})</h3>
      <template v-if="dataKelas.length">
        <ul>
          <li v-for="(item, index) in dataKelas" :key="index">
            {{ index + 1 }} - {{ item }} | <a href="#" v-on:click.prevent="hapusKelas(index)">hapus</a>
          </li>
        </ul>
      </template>
      <p v-else>Kelas belum tersedia</p>
    </div>
  `,
  data() {
    return {
      dataKelas: ["PHP", "HTML CSS"],
      kelasBaru: ""
    };
  },
  methods: {
    hapusKelas(index) {
      this.dataKelas.splice(index, 1);
    },
    tambahKelas() {
      if (this.kelasBaru) {
        this.dataKelas.unshift(this.kelasBaru);
        this.kelasBaru = "";
      }
    }
  }
};

const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  { path: '/kelas', component: Kelas }
];

const router = new VueRouter({
  routes
});

const app = new Vue({
  el: '#app',
  router
});
</script>
</body>
</html>
