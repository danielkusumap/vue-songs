<template>
  <div>
    <h6 class="text-center">
      Menampilkan {{ hasil }} hasil untuk pencarian: {{ artist }}
    </h6>
    <b-container
      class="bv-example-row justify-content-center"
      v-if="output.lenght != 0"
    >
      <b-row>
        <b-col cols="4" v-for="i in output" :key="i.title">
          <div class="d-flex justify-content-center mt-3 p-3 w-100">
            <b-card
              :title="artist"
              :img-src="getThumnailURL(i.ytMusic_URL)"
              tag="article"
              style="font-size: 2vw; max-width: 20rem"
              class="mb-2 w-100 text-center test"
            >
              <div style="font-size: 1vw">
                <b-card-text> {{ i.title }} </b-card-text>
                <b-card-text> {{ i.year_release }} </b-card-text>
                <div
                  v-if="
                    i.ytMusic_URL != 'belum' &&
                    i.ytMusic_URL != 'link not found'
                  "
                >
                  <b-button
                    :href="i.ytMusic_URL"
                    target="_blank"
                    variant="primary"
                    class="d-flex justify-content-center"
                    >dengar di yt music</b-button
                  >
                </div>
                <div v-else>
                  <b-button
                    href="#"
                    target="_blank"
                    variant="primary"
                    disabled
                    class="d-flex justify-content-center"
                    >link not found</b-button
                  >
                </div>
              </div>
            </b-card>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "TampilOutput",
  data() {
    return {
      hasil: this.output.length,
    };
  },
  props: {
    output: Array,
    artist: String,
  },
  methods: {
    getThumnailURL(ytMusic_URL) {
      var id = ytMusic_URL.split(/[=&]/)[1];
      return "https://img.youtube.com/vi/" + id + "/hqdefault.jpg";
    },
  },
};
</script>

<style>
.test{
  transition: box-shadow .3s;
}
.test:hover {
  box-shadow: 0 0 30px rgba(12, 147, 226, 0.425); 
}
</style>