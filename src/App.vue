<template>
  <div>

    <dialog class="modal" id="modal">
      <p>{{ fact }}</p>
      <button class="button close-button" @click="closeModal">close</button>
    </dialog>

    <h1>CATS IN CARDS IN VUE.JS</h1>

    <div class="wrapper">
      <div 
      v-for="cat of cats" 
      :key="cat.breed" 
      @click="randomFact">
        <CatCard
          :img="require('./assets/shadow-cat.jpg')"
          :title="cat.breed"
          :coat="cat.coat"
          :pattern="cat.pattern"
        />
      </div>
    </div>
    
  </div>
</template>


<script>
import CatCard from "./components/CatCard.vue";

export default {

  name: "App",
  components: {
    CatCard,
  },

  data() {
    return {
      cats: [],
      fact: "",
    };
  },

  async created() {
    try {
      const data = await fetch("https://catfact.ninja/breeds");
      const body = await data.json();
      this.cats = body.data;
    } catch (e) {
      console.error(e);
    }
  },

  methods: {
    randomFact: async function () {
      try {
        const data = await fetch("https://catfact.ninja/fact");
        const body = await data.json();
        this.fact = body.fact;
      } catch (e) {
        console.error(e);
      }
      document.querySelector("#modal").showModal();
    },
    closeModal: function () {
      document.querySelector("#modal").close();
    },
  },
};
</script>


<style lang="scss">
@import "@/styles/app.scss";
@import "@/styles/modal.scss";
</style>
