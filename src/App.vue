<template>
  <div id="app">
    <SearchField @input="cariInput" :years_list="years_list" />
    <TampilOutput
      v-if="cekData == 'ada'"
      :output="output"
      :artist="artist"
      :years_list="years_list"
    />
    <b-alert
      v-else-if="cekData == 'kosong'"
      class="w-50 m-auto mt-2"
      show
      variant="danger"
      >{{ artist }} not found</b-alert
    >
  </div>
</template>

<script>
import SearchField from "./components/SearchField.vue";
import TampilOutput from "./components/Output.vue";
import axios from "axios";
export default {
  components: {
    SearchField,
    TampilOutput,
  },
  data() {
    return {
      output: [],
      years_list: [],
      artist: "",
      cekData: "",
    };
  },
  methods: {
    cariInput(url, artist) {
      this.cekData = "";
      if (artist != "kosong") {
        this.artist = artist;
      }

      axios.get(url).then((r) => {
        if (Array.isArray(r.data.output)) {
          this.cekData = "ada";
          this.output = r.data.output;
          if (artist != "kosong") {
            this.years_list = r.data.years_list;
          }
        } else {
          this.cekData = "kosong";
        }
      });
    },
    tampilOutput(output) {
      this.output = output;
      console.log(output);
    },
  },
};
</script>

<style>
</style>