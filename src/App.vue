<template>
  <div id="app" style="display: flex; height: 100vh">
    <div>
      <b-progress
        v-show="show"
        :value="value"
        :max="max"
        height="5px"
        :striped="true"
      ></b-progress>
      <SideBar :recent="recent"/>
      <!-- <div v-show="recent.length">
        <b-button v-b-toggle.sidebar-1>Recent</b-button>
        <b-sidebar ref="close" id="sidebar-1" title="Recent" shadow>
          <div class="px-3 py-2">
            <b-form-checkbox switch>Default</b-form-checkbox>
            <div v-for="i in recent" :key="i" class="m-2">
              <b-button variant="outline-info" @click="close(i)">{{
                i
              }}</b-button>
            </div>
          </div>
        </b-sidebar>
      </div> -->
    </div>

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
import SideBar from "./components/SideBar.vue"
import axios from "axios";
export default {
  components: {
    SearchField,
    TampilOutput,
    SideBar
  },
  data() {
    return {
      output: [],
      years_list: [],
      artist: "",
      cekData: "",
      value: 0,
      max: 100,
      show: false,
      recent: [],
      test: "hidden",
    };
  },
  methods: {
    async cariInput(url, artist) {
      document.getElementById("app").style = "";
      this.show = true;
      this.cekData = "";
      if (artist != "kosong") {
        this.artist = artist;
      }
      this.value = 75;

      await axios.get(url).then((r) => {
        if (Array.isArray(r.data.output)) {
          this.cekData = "ada";
          this.output = r.data.output;
          if (artist != "kosong") {
            this.years_list = r.data.years_list;
          }
        } else {
          this.cekData = "kosong";
        }
        this.value = 100;
        this.show = false;
        this.value = 0;
      });
      if (this.cekData == "ada") {
        if (this.recent.includes(artist)) {
          this.recent.splice(this.recent.indexOf(artist), 1);
        }
        if (!this.recent.includes(artist)) {
          this.recent.unshift(artist);
        }
      }
    },
    tampilOutput(output) {
      this.output = output;
    }
  },
};
</script>

<style>
/* #app{
  display: flex;
  height: 100vh;
} */
</style>