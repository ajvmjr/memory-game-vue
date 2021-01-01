<template>
  <v-card
    flat
    outlined
    class="card"
    height="300px"
    @click="handleClick"
    :disabled="card.disabled"
  >
    {{ card.value }}
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
  background-color: #ffd045;
  background-image: linear-gradient(315deg, #ffd045 0%, #d14545 74%);
  border: 2px solid #fff !important;
  width: 250px;

  &--selected {
    background: blue !important;
  }
}
</style>
