<template>
  <div id="app">
    <v-app>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            sm="6"
            md="3"
            lg="3"
            v-for="c in cards"
            :key="c.id"
            class="d-flex justify-center"
          >
            <Card
              @selected="handleClick($event)"
              :info="c"
              :disabled="disabled"
            />
          </v-col>
        </v-row>
      </v-container>
      <Modal
        @updateDifficult="updateDifficult($event)"
        @close="closeModal"
        :title="dialogTitle"
        :dialog="dialog"
      />
    </v-app>
  </div>
</template>

<script>
import Card from "@/components/Card";
import Modal from "@/components/Modal";

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
      {
        id: 9,
        value: "5",
        chosen: false,
        disabled: false,
      },
      {
        id: 10,
        value: "5",
        chosen: false,
        disabled: false,
      },
      {
        id: 11,
        value: "6",
        chosen: false,
        disabled: false,
      },
      {
        id: 12,
        value: "6",
        chosen: false,
        disabled: false,
      },
      {
        id: 13,
        value: "7",
        chosen: false,
        disabled: false,
      },
      {
        id: 14,
        value: "7",
        chosen: false,
        disabled: false,
      },
      {
        id: 15,
        value: "8",
        chosen: false,
        disabled: false,
      },
      {
        id: 16,
        value: "8",
        chosen: false,
        disabled: false,
      },
    ],
    corrects: [],
    cardsChosen: [],
    gameEnded: false,
    disabled: false,
    dialog: true,
    dialogTitle: "Olá! Selecione o nível que deseja jogar.",
  }),

  name: "App",
  components: { Card, Modal },

  watch: {
    gameEnded() {
      if (this.gameEnded) {
        this.cards = [
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
          {
            id: 9,
            value: "5",
            chosen: false,
            disabled: false,
          },
          {
            id: 10,
            value: "5",
            chosen: false,
            disabled: false,
          },
          {
            id: 11,
            value: "6",
            chosen: false,
            disabled: false,
          },
          {
            id: 12,
            value: "6",
            chosen: false,
            disabled: false,
          },
          {
            id: 13,
            value: "7",
            chosen: false,
            disabled: false,
          },
          {
            id: 14,
            value: "7",
            chosen: false,
            disabled: false,
          },
          {
            id: 15,
            value: "8",
            chosen: false,
            disabled: false,
          },
          {
            id: 16,
            value: "8",
            chosen: false,
            disabled: false,
          },
        ];
        this.cards.map((card) => {
          card.chosen = false;
          card.disabled = false;
        });
        this.gameEnded = false;
      }
    },
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
          }, 1000);
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

    updateDifficult(e) {
      this.cards.map((card) => {
        card.chosen = false;
        card.disabled = false;
      });

      const difficulties = ["Fácil", "Médio", "Difícil"];
      const selected = difficulties[e.id - 1];

      if (selected === "Fácil") {
        this.cards = this.cards.slice(0, 8);
      } else if (selected === "Médio") {
        this.cards = this.cards.slice(0, 12);
      }
      this.shuffle();
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
      this.gameEnded = true;
      this.cards.map((card) => {
        card.chosen = false;
        card.disabled = false;
      });

      this.cardsChosen = [];
      this.corrects = [];
      this.disabled = false;
      this.dialog = true;

      this.dialogTitle = "Parabéns, você venceu! Deseja jogar novamente?";
    },

    closeModal() {
      this.dialog = false;
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
  background: rgba(0, 0, 0, 0.9);
}
</style>
