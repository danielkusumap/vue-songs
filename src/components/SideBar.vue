<template>
  <div v-show="recent.length">
    <b-button  v-b-toggle.sidebar-1>Recent</b-button>
    <b-sidebar ref="close_sidebar" id="sidebar-1" title="Recent" shadow>
      <div class="px-3 py-2">
        <b-form-checkbox
          id="checkbox-1"
          v-model="status"
          name="checkbox-1"
          value="ON"
          unchecked-value="OFF"
          >{{status}}</b-form-checkbox
        >
        <div v-for="i in recent" :key="i" class="m-2">
          <b-button variant="outline-info" @click="close(i)">{{ i }}</b-button>
        </div>
      </div>
    </b-sidebar>
  </div>
</template>

<script>
export default {
  name: "SideBar",
  props: {
    recent: Array,
  },
  data(){
    return{
      status: "OFF"
    }
  },
  methods: {
    close(artist) {
      if(this.status === "ON"){
          this.$refs.close_sidebar.hide();
      }
      
      document.getElementById("input_artist_form").value = artist;
      document.getElementById("cariArtist").click();
    }
  },
};
</script>

<style>
</style>