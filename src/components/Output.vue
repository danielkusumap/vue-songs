<template>
  <div>
    <b-container
      class="bv-example-row justify-content-center"
      v-if="output.lenght != 0"
    >
      <b-row>
        <b-col cols="4" v-for="i in output" :key="i.title">
          <div class="d-flex justify-content-center mt-3 p-3 w-100 test">
            <b-card
              :title="artist"
              tag="article"
              style="max-width: 20rem"
              class="mb-2 w-100 text-center"
            >
              <b-card-text> {{ i.title }} </b-card-text>
              <b-card-text> {{ i.year_release }} </b-card-text>
              <div v-if="i.ytMusic_URL != 'belum' && i.ytMusic_URL != 'link not found'">
                <b-button
                  :href="i.ytMusic_URL"
                  target="_blank"
                  variant="primary"
                  >dengar di yt music</b-button
                >
              </div>
              <div v-else>
                <b-button
                  href="#"
                  target="_blank"
                  variant="primary"
                  disabled
                  >link not found</b-button
                >
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
  props: {
    output: Array,
    artist: String
  }
};
</script>

<style>
.test{
    font-size: 12pt;
}
</style>