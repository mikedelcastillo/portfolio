<script>
const URL = "https://script.google.com/macros/s/AKfycbyX21heSXPizeIFz9OY4Sv4PvM9MO5YPLbk1SjW-JR2aQ044w/exec";

export default {
  name: 'app',
  data() {
    return {
      loading: true,
      items: []
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load(){
      this.loading = true;
      this.$http.get(URL)
      .then(({data}) => {
        this.items = data;
        this.loading = false;
      })
      .catch(e => {});
    }
  }
}
</script>

<style lang="sass">

@import ../sass/defaults

</style>


<template lang="pug">

  .screen
    .screen(v-show="loading")
      #loading-wrapper
        .spinner-wrapper
          .mask
            .circle
    .screen(v-show="loading == false")
      #splash-wrapper
        .background-image
          .byline Photo by Arcel Vocales
        .center-wrapper
          .text-wrapper
            .name-wrapper
              .nickname Mike
              .lastname del Castillo
            .description Full-stack<span>+</span>Designer
        .email-wrapper
          a.email(href="mailto:hello@mikedc.io") hello@mikedc.io
      #items-wrapper
        .center-wrapper
          a.item(v-for=`item in items` v-bind:href=`item.url` target="_blank")
            .image-wrapper
              .image(:style=`{backgroundImage: "url(img/previews/" + item.id + ".jpg)"}`)
              .sizer
            .details-wrapper
              .name {{item.name}}
              .domain {{item.domain}}
</template>
