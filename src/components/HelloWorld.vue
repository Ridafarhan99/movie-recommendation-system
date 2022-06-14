<template  class="background">
  <div>
  <h1
  elevation="12"
  style="text-align:center; margin-top: 80px;"
  class="header"
  >Movie Recommendation System</h1>
  <div class="fill-height bottom-gradient"></div>
  


</div>
</template>

<script>
  export default {
    data(){
      
    },
    watch:{
      // search () {
      //   // Items have already been loaded
      //   if (this.items.length > 0) return

      //   // Items have already been requested
      //   if (this.isLoading) return

      //   this.isLoading = true

      //   // Lazily load input items
      //   fetch(this.SEARCH_API+this.moviename)
      //     .then(res => res.json())
      //     .then(res => {
      //       const { page, results } = res
      //       this.page = page
      //       this.entries = results
      //     })
      //     .catch(err => {
      //       console.log(err)
      //     })
      //     .finally(() => (this.isLoading = false))
      // },
    }
  }
</script>

<style>
.autocompleteinput{
  width: 30%;
  align-self: center;
}
.header{
  text-align: center;
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-size: 55px;
  color: red;
  text-shadow: 3px 4px 6px black, 0 0 0.3em black, 0 0 0.3em black;
}

</style>