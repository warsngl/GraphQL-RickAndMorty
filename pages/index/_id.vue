<template lang='pug'>
.flex.flex-col.border.shadow(v-if='character' class='sm:text-lg xl:flex-row xl:text-6xl')
  img(:src='character.image')
  .bio
    p {{character.name}}
    span.text-xl {{character.gender}} - {{character.species}}
</template>

<script>
import character from '@/apollo/query/character'
export default {
  data:()=>({
    character:{},
  }),
  apollo:{
    character:{
      query: character,
      prefetch:false,
      variables(){
        if(this.id){
          return {id:this.id}
        }else{
          this.$router.push('/1')
          return {id:1}
        }
      }
    },
  },
  computed:{
    id(){
      return this.$route.params.id
    },
  }

}
</script>

<style>

</style>