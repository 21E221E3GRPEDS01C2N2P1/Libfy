
<template>
  <div class="navbb">
    <div class="sidenav" :class="esconderSideBar ? 'd-none' : ''">
      <router-link to="/" :class="
      atualRota === 'Home' ?
      'purple white--text'  : '' ">
        <span class="fa fa-home"></span> Home
      </router-link>
      <router-link to="/pesquisa" :class="
      atualRota === 'Pesquisa' ?
      'purple white--text'  : '' ">
        <span class="fa fa-search"></span> Pesquisa
      </router-link>
      <router-link to="/noticias" :class="
      atualRota === 'Noticias' ?
      'purple white--text'  : '' ">
        <span class="fa fa-news"></span> Noticias
      </router-link>

      <section v-if="user.loggedIn">
        <div v-if="false">
          <!-- to do -->
          <router-link to="/login">
            <span class="fas fa-music"></span>
            <p>Playlists</p>
          </router-link>
          <a href="index.html" class="botao">
            <span class="fas fa-heart"></span>
            <p>Notícias</p>
          </a>
        </div>
        <v-container>
          <h6>Your Library</h6>
          <p>Favoritas</p>
          <p>Favoritas</p>
        </v-container>
      </section>
    </div>
    <section class="topofixo d-flex flex-row justify-start align-center">
      <div class="pesquisa">
        <i class="fa fa-search icone" aria-hidden="true"></i>
        <input
          type="text"
          placeholder="Artists,songs or podcasts"
          v-on:keyup.enter="pesquisarMusica"
          v-model="pesquisatex"
        />
      </div>
      <div :class="esconderSideBar ? 'd-none' : ''">
        <main v-if="user.loggedIn" class="d-flex flex-row transparent">
          <v-btn rounded dark to="/perfilusuario" >
          <div class="reduzbotao">{{ gNomeUsuario }}</div>  </v-btn>
        </main>

        <main v-else class="d-flex flex-row transparent">
          <v-btn rounded color="primary" dark to="/cadastrar" 
          class="reduzbotao">
            Cadastrar
          </v-btn>
          <v-btn rounded to="/login" class="reduzbotao"> Log in </v-btn>
        </main>
      </div>
    </section>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Navbar",
  props: ["esconderSideBar"],
  data: () => {
    return {
      pesquisatex: ""
    };
  },
  computed: {
    atualRota() {
      return this.$route.name;
    },
    ...mapGetters({
      user: "getUser",
      getQualquerCois: "getQualquerCois",
      gNomeUsuario: "getNomeUsuario",
      gPesqR: "getPesquisaResult"
    })
  },
  methods: {
    pesquisarMusica(e) {
      this.$store.commit("SET_PESQUISAQUERY", this.pesquisatex);
      console.log(`${this.$route.name}`);

      if (this.$route.name === "Pesquisa") {
        this.$store.dispatch("pesquisaMusica");
        return;
      }

      this.$router.push({ name: "Pesquisa" });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@import "css/Navbar.scss";
</style>
