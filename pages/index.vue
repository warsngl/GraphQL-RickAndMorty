<template lang='pug'>
.w-full.flex.flex-wrap
  TheLoading(v-if='isLoading')
  TheCard(v-else v-for='c,idx in chars' :key='c.id' :c='c')
</template>

<script>
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
      try{
        await this.$axios.get('https://rickandmortyapi.com/api/character')
        .then(r=>{
          this.chars=r.data.results})
      }catch{
        console.log(e);
      }finally{
        this.isLoading=false
      }
      //const chars=await gql
    }
  }
}
</script>

<style>

</style>