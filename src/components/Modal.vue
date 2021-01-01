<template>
  <v-dialog
    v-model="showModal"
    transition="dialog-bottom-transition"
    width="520"
  >
    <v-card class="dialog">
      <v-card-title>{{ title }}</v-card-title>
      <v-card-text>
        <v-select
          :items="difficults"
          label="Selecione a dificuldade"
          item-text="name"
          item-value="id"
          return-object
          v-model="difficultSelected"
          @change="updateDifficult"
        />

        <v-card-actions class="dialog__actions">
          <v-btn
            class="dialog__actions__buttons"
            width="100"
            @click="closeModal"
            >Ok</v-btn
          >
        </v-card-actions>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    difficults: [
      {
        id: 1,
        name: "Fácil (8)",
      },
      {
        id: 2,
        name: "Médio (12)",
      },
      {
        id: 3,
        name: "Difícil (16)",
      },
    ],
    difficultSelected: {},
    showModal: false,
  }),

  props: {
    dialog: Boolean,
    title: String,
  },

  watch: {
    dialog() {
      this.showModal = this.dialog;
    },
  },

  mounted() {
    this.showModal = this.dialog;
  },

  methods: {
    updateDifficult() {
      this.$emit("updateDifficult", this.difficultSelected);
      this.difficultSelected = {};
    },

    closeModal() {
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped>
.dialog {
  &__actions {
    display: flex;
    justify-content: flex-end;
    &__buttons {
      color: white !important;
      font-weight: 500 !important;
      background-color: #ffd045;
      background-image: linear-gradient(315deg, #ffd045 0%, #d14545 74%);
    }
  }
}
</style>
