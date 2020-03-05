<template>
  <v-container fill-height>
    <v-layout fill-height align-center justify-center>
      <v-btn color="primary" class="ma-4" @click="dialog = true">
        Open Scanner
      </v-btn>
    </v-layout>
    <v-dialog v-model="dialog" fullscreen="" max-width="500px">
      <v-card class="d-flex flex-column">
        <v-card-title>Scan The barcode</v-card-title>
        <v-card-text class="flex-grow-1">
          <v-layout
            v-if="dialog && !result"
            fill-height
            align-center
            justify-center
          >
            <VueQrReader
              vide-width="320"
              vide-height="640"
              @code-scanned="onCode"
            ></VueQrReader>
          </v-layout>
          <div v-else class="w-100">
            <h4>Result</h4>
            <p class="border pa-3">
              {{ result }}
            </p>
          </div></v-card-text
        >
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="dialog = false">close</v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import VueQrReader from "vue-qr-reader/dist/lib/vue-qr-reader.umd.js";

export default {
  name: "Home",
  components: { VueQrReader },
  data: () => ({
    dialog: false,
    result: ""
  }),
  watch: {
    dialog() {
      this.result = "";
    }
  },
  methods: {
    onCode(code) {
      this.result = code;
    }
  }
};
</script>

<style lang="scss">
.vue-qr-reader__container {
  canvas {
    width: 100%;
    height: auto;
    max-width: 320px;
  }
}
.border {
  border: 1px solid black;
}
</style>
