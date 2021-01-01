<template>
  <v-card
    flat
    outlined
    class="card"
    :class="cards[index].chosen ? 'card card--selected' : 'card'"
    :disabled="disabled"
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
      },
      {
        id: 2,
        value: "1",
        chosen: false,
      },
      {
        id: 3,
        value: "2",
        chosen: false,
      },
      {
        id: 4,
        value: "2",
        chosen: false,
      },
      {
        id: 5,
        value: "3",
        chosen: false,
      },
      {
        id: 6,
        value: "3",
        chosen: false,
      },
      {
        id: 7,
        value: "4",
        chosen: false,
      },
      {
        id: 8,
        value: "4",
        chosen: false,
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
  background: yellow !important;
  border: 2px solid #fff !important;
  width: 250px;

  &--selected {
    background: blue !important;
  }
}
</style>
