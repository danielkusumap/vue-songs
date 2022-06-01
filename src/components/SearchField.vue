<template>
  <div
    class="
      d-flex
      justify-content-center
      m-auto
      p-2
      pt-3
      sticky-top
      bg-white
      test
    "
  >
    <div class="me-2 w-50">
      <b-form-input
        v-model="inputArtist"
        placeholder="Enter artist name"
        v-on:keyup.enter="sendInput"
      ></b-form-input>
    </div>
    <div>
      <b-button class="me-2" variant="primary" @click="sendInput"
        >Cari</b-button
      >
    </div>
    <div>
      <b-button class="me-2" v-b-modal.modal-center>Filter</b-button>

      <b-modal
        id="modal-center"
        centered
        title="Filter"
        @ok="ok"
        @onlyYear="onlyYear"
        @GTEYear="GTEYear"
      >
        <b-button
          variant="outline-primary"
          class="me-2 mb-2"
          @click="onlyYear()"
          :pressed.sync="only_year"
        >
          only year
        </b-button>
        <b-button
          variant="outline-primary"
          class="me-2 mb-2"
          @click="GTEYear()"
          :pressed.sync="gte_year"
        >
          greater than equal
        </b-button>
        <b-form-select
          v-model="selected"
          :options="years_list"
          class="mb-3 w-100"
        >
          <template #first>
            <b-form-select-option :value="null" disabled
              >-- Please select an option --</b-form-select-option
            >
          </template>
        </b-form-select>
        <template #modal-footer="{ ok, cancel }">
          <b-button size="sm" variant="primary" @click="ok()"> OK </b-button>
          <b-button size="sm" variant="danger" @click="cancel()">
            Cancel
          </b-button>
        </template>
      </b-modal>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchField",
  props: {
    years_list: Array,
  },
  data() {
    return {
      inputArtist: "",
      selected: null,
      only_year: true,
      gte_year: false,
      final_year: false,
    };
  },
  methods: {
    sendInput() {
      var url = "http://127.0.0.1:5000/api?artist=" + this.inputArtist;
      this.$emit("input", url, this.inputArtist);
    },
    ok() {
      var url =
        "http://127.0.0.1:5000/api?artist=" +
        this.inputArtist +
        "&year=" +
        this.selected.toString() +
        "&yearGTE=" +
        this.final_year;
      this.$emit("input", url, "kosong");
    },
    onlyYear() {
      this.only_year = true;
      this.gte_year = false;
      this.final_year = false;
    },
    GTEYear() {
      this.only_year = false;
      this.gte_year = true;
      this.final_year = true;
    },
  },
};
</script>

<style>
</style>