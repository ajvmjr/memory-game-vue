<template>
  <div id="app">
    <v-container>
      <v-row>
        <v-col cols="12" lg="3" v-for="c in cards" :key="c.id">
          <Card
            @selected="handleClick($event)"
            :info="c"
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
    cards: [
      {
        id: 1,
        value: "1",
        chosen: false,
        disabled: false,
      },
      {
        id: 2,
        value: "1",
        chosen: false,
        disabled: false,
      },
      {
        id: 3,
        value: "2",
        chosen: false,
        disabled: false,
      },
      {
        id: 4,
        value: "2",
        chosen: false,
        disabled: false,
      },
      {
        id: 5,
        value: "3",
        chosen: false,
        disabled: false,
      },
      {
        id: 6,
        value: "3",
        chosen: false,
        disabled: false,
      },
      {
        id: 7,
        value: "4",
        chosen: false,
        disabled: false,
      },
      {
        id: 8,
        value: "4",
        chosen: false,
        disabled: false,
      },
    ],
    corrects: [],
    cardsChosen: [],
    disabled: false,
  }),

  name: "App",
  components: { Card },

  created() {
    this.shuffle();
  },

  methods: {
    handleClick(e) {
      let { cardsChosen } = this;
      if (cardsChosen.length < 2) {
        cardsChosen.push(e);
      }

      if (cardsChosen.length === 2) {
        this.disabled = true;
        if (cardsChosen[0].value === cardsChosen[1].value) {
          setTimeout(() => {
            this.correct();
            this.corrects.push(cardsChosen[0], cardsChosen[1]);
            this.checkWin();
          }, 2000);
        } else {
          setTimeout(() => {
            this.resetCurrentCards();
          }, 2000);
        }
      }
    },

    shuffle() {
      for (let i = this.cards.length - 1; i >= 0; i--) {
        const j = Math.floor(Math.random() * i);
        const temp = this.cards[i];
        this.cards[i] = this.cards[j];
        this.cards[j] = temp;
      }
    },

    checkWin() {
      if (this.corrects.length === this.cards.length) {
        setTimeout(this.resetGame(), 3000);
      }
    },

    correct() {
      this.cardsChosen = [];
      this.disabled = false;
    },

    resetCurrentCards() {
      this.cardsChosen[0].chosen = false;
      this.cardsChosen[1].chosen = false;
      this.cardsChosen[0].disabled = false;
      this.cardsChosen[1].disabled = false;
      this.cardsChosen = [];
      this.disabled = false;
    },

    resetGame() {
      this.cardsChosen = [];
      this.corrects = [];
      this.disabled = false;

      this.cards.map((card) => {
        card.chosen = false;
        card.disabled = false;
      });
      this.shuffle();
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
  background: rgba(0, 0, 0, 0.9);
}
</style>
