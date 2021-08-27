<template>
  <h1>MUTATIONS</h1>
  <button @click="increment">Increment +1</button>
  <button @click="incrementBy">Increment +5</button>
  <button @click="incrementRandom" :disabled="isLoading">Increment random</button>
  
  
  <h1>STATE con VUEX</h1>
  <h2>Direct acces: {{$store.state.counter.count}}</h2>
  <p>{{$store.state.counter.lastMutation}}</p>

  <h2>Computed: {{getCounter}}</h2>
  <p>{{getLastMutation}}</p>

  <h2>mapState: {{count}}</h2>
  <p>{{lastMutation}}</p>

  <h2>MapStateObject:{{counter}}</h2>
  <p>{{lastMutation2}}</p>

  <h1>GETTERS</h1>
  <h2>Direct getter:{{$store.getters["counter/squareCount"]}} </h2>
</template>

<script>
import { mapActions, mapState } from 'vuex'
export default {
  
  methods:{
    increment(){
      this.$store.commit("counter/increment")
    },
    incrementBy(){
      this.$store.commit("counter/incrementBy",5)
    },
    // incrementByRandom(){
    //   this.$store.dispatch("incrementRandom")
    // }
    ...mapActions("counter",["incrementRandom"])
  },
  computed:{
    getCounter(){
      return this.$store.state.counter.count
    },
    getLastMutation(){
      return  this.$store.state.counter.lastMutation
    },
    ...mapState("counter",["count","lastMutation","isLoading"]),
    ...mapState("counter",{
      counter:state=>state.count,
      lastMutation2:state=>state.lastMutation
    }),
    
  }
}
</script>

<style>

</style>