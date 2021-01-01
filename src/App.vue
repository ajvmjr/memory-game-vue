<template>
  <div id="app">
    <v-container>
      <v-row>
        <v-col cols="12" lg="3" v-for="(x, index) in 8" :key="index">
          <Card
            @selected="handleClick($event)"
            :index="index"
            :disabled="disabled"
          />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import Card from "@/components/Card";

export default {
  data: () => ({
    cardsChosen: [],
    disabled: false,
  }),

  name: "App",
  components: { Card },

  methods: {
    handleClick(e) {
      let { cardsChosen } = this;
      if (cardsChosen.length < 2) {
        this.disabled = false;
        cardsChosen.push(e);
      }

      if (cardsChosen.length === 2) {
        this.disabled = true;
        if (cardsChosen[0].value === cardsChosen[1].value) {
          setTimeout(() => {
            this.correct();
          }, 2000);
        } else {
          setTimeout(() => {
            this.reset();
          }, 2000);
        }
      }
    },

    correct() {
      this.cardsChosen = [];
      this.disabled = false;
    },

    reset() {
      this.cardsChosen[0].chosen = false;
      this.cardsChosen[1].chosen = false;
      this.cardsChosen = [];
      this.disabled = false;
    },
  },
};
</script>

<style lang="scss">
#app,
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  height: 100vh;
  // background: #0a0e42;
  background: rgb(148, 131, 131);
}
</style>
