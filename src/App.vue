<template>
  <div>
    <router-view v-if="$store.state.ready" />
    <template v-else>
      <div class="chargement has-text-light">
        <p>Chargement, veuillez patienter</p>
        <button class="button is-loading is-dark"></button>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  data() {
    return {
      loaded: false
    }
  },
  mounted() {
    this.$store.commit("setReady", true);
    // si le token n'est pas présent renvoyer vers la connexion
    if (!this.$store.state.token) {
      this.seConnecter();
    } else {
      // if(this.$store.state.member.role == 100){   //empêcher un inviter d'accéder à l'Acceuil
      //   this.$router.push("/Accueil");
      // }
      //  this.$router.push("/Accueil");
    }
  },
  methods: {
    seConnecter() {
      this.$store.commit("setToken", false);
      this.$store.commit("setMember", false);
      this.$router.push("/");
      this.ready();
    },
    ready() {
      this.$store.commit("setReady", true);
    },
  },
};
</script>
<style lang="scss">
body {
  background-color: hsl(124, 12%, 48%);
}
</style>
