<template lang="pug">
  #app
    .block
      input(
        v-model="searchedUrl"
      )
      button(
        @click="getImageByUrl"
      ) Submit

    .block.image-wrap(
      ref="wrap"
    )
      img.img(
        :src="imageUrl"
        @load="imageOnload"
        :width="imageWidth"
        :height="imageHeight"
      )

</template>

<script>


export default {
  name: 'App',
  data: function () {
    return {
      searchedUrl: "",
      imageUrl: "",
      wrapWidth: 0,
      wrapHeight: 0,
      isWidthBigger: false
    }
  },
  computed: {
    imageWidth(){
      return this.isWidthBigger ? this.wrapWidth : this.wrapHeight * (4/5)
    },
    imageHeight(){
      return this.isWidthBigger ? this.wrapWidth * (9/16) : this.wrapHeight
    }
  },
  mounted() {
    this.wrapWidth = this.$refs.wrap.offsetWidth
    this.wrapHeight = this.$refs.wrap.offsetHeight
    window.addEventListener("resize",  ()=> {
      this.wrapWidth = this.$refs.wrap.offsetWidth
      this.wrapHeight = this.$refs.wrap.offsetHeight
    })
  },
  methods: {
    getImageByUrl(){
      this.imageUrl = this.searchedUrl
    },
    imageOnload(e){
      let newWidth = e.target.offsetWidth
      let newHeight = e.target.offsetHeight
      this.isWidthBigger = newWidth > newHeight ? true : false
    },

  }
}
</script>

<style>
  @import "../node_modules/reset-css/reset.css";
  #app{
    display: flex;
  }
  .block{
    width: 50%;
  }
  .image-wrap{
    height: 50vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: red;

  }

</style>
