<template lang='pug'>
.w-full.flex.flex-wrap
  TheLoading(v-if='isLoading')
  TheCard(v-else v-for='c,idx in chars' :key='c.id' :c='c')
</template>

<script>
import gql from 'graphql-tag'
const chars=gql`
  query chars($page: Int!, $filter: FilterCharacter!) {
    characters(page: $page, filter: $filter) {
      info {
        count
        pages
      }
      results {
        id
        name
        image
        species
        status
        type
      }
    }
  }
`
export default { 
  data:()=>({
    chars:[],
    isLoading:false,
  }),
  async mounted(){
    await this.fetchAll()
  },
  methods:{
    async fetchAll(){
      this.isLoading=true
      // try{
      //   await this.$axios.get('https://rickandmortyapi.com/api/character')
      //   .then(r=>{
      //     this.chars=r.data.results})
      // }catch(e){
      //   console.log(e);
      // }finally{
      //   this.isLoading=false
      // }
    }
  }
}
</script>

<style>

</style>