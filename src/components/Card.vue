<template>
  <v-card
    flat
    outlined
    class="card"
    height="300px"
    @click="handleClick"
    :disabled="disabled || card.disabled"
  >
    <p v-if="card.chosen" class="card__value">{{ card.value }}</p>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    card: {},
  }),

  props: {
    info: Object,
    disabled: Boolean,
  },

  watch: {
    info: {
      handler() {
        this.card = this.info;
      },
      deep: true,
    },
  },

  mounted() {
    this.card = this.info;
  },

  methods: {
    handleClick() {
      this.card.chosen = true;
      this.card.disabled = true;
      this.$emit("selected", this.card);
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  align-items: center;
  background-color: #ffd045;
  background-image: linear-gradient(315deg, #ffd045 0%, #d14545 74%);
  border: 2px solid #fff !important;
  display: flex;
  justify-content: center;
  width: 250px;

  &--selected {
    background: blue !important;
  }

  &__value {
    color: white;
    font-size: 100px;
    font-weight: 800;
  }
}
</style>
