<template lang='pug'>
.w-screen.h-screen.p-0.bg-gray-200(class='sm:p-1 lg:py-4 lg:px-2 xl:py-4 xl:px-4')
  button(class='button--green' :disabled='!characters' @click.stop='showAll') {{buttonText}}
  ul.absolute.z-10.overflow-scroll.overflow-x-hidden(v-if='isExpanded' class='bg-purple-200 rounded shadow w-64')
    li.py-2(v-for='character in characters.results' :key='character.id' class='rounded text-center')
      nuxt-link(:to='character.id.toString()' class='hover:font-bold') {{character.name}}
  .flex-grow.bg-white
    nuxt-child
</template>

<script>
import characters from '@/apollo/query/characters'

import gql from 'graphql-tag'
export default { 
  data:()=>({
    isLoading:false,
    character:{},
    isExpanded:false,
  }),
  apollo:{
    characters: {
      query: characters
    },
  },
  methods:{
    getAll(){
      this.$apollo.query({query: characters}).then(data=>{
        this.characters=data
      })
    },
    getChar(){
      this.$apollo.query({query:character}).then(data=>{
        this.character=data
      })
    },
    showAll(){
      this.isExpanded=!this.isExpanded
    }
  },
  computed:{
    buttonText(){
      return this.isExpanded?'Close':'Show'
    }
  }
}
</script>

<style>
ul{
  height: 75%;
}
</style>