<template>
  <v-card
    flat
    outlined
    class="card"
    :class="cards[index].chosen ? 'card card--selected' : 'card'"
    :disabled="disabled || cards[index].disabled"
    height="300px"
    @click="handleClick"
  >
  </v-card>
</template>

<script>
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
  }),

  props: {
    index: Number,
    disabled: Boolean,
  },

  methods: {
    handleClick() {
      this.selectCards();
    },

    selectCards() {
      if (!this.cards[this.index].chosen) {
        this.cards[this.index].chosen = true;
        this.cards[this.index].disabled = true;
        this.$emit("selected", this.cards[this.index]);
      } else {
        this.cards[this.index].chosen = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  background-color: #ffd045;
  background-image: linear-gradient(315deg, #ffd045 0%, #d14545 74%);
  border: 2px solid #fff !important;
  width: 250px;

  &--selected {
    background: blue !important;
  }
}
</style>
