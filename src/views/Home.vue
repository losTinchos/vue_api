<template>
  <div class="home">
    <h1>{{text}}</h1>
    <div class="flex flex-wrap justify-center text-red-600">
      <div v-for="subscribers in eventSubscribers" :key="subscribers">{{subscribers.name}}</div>

      <Event v-for="event in events" :key="event.id" :event="event" :date="event.date"
    :title="event.title" :capacity="event.capacity" :description="event.description" 
    :method="event.showSubscribers" />
      
   

  </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Event from '@/components/Event.vue'

import axios from 'axios'
export default {
  name: 'Home',
  components: {HelloWorld, Event}, 
  
 
 data(){
    return{
      events:[],
      eventSubscribers: [],
      text:'Events',
    }
},

mounted(){
    axios.get('http://127.0.0.1:8000/api/events').then
    (response => {this.events = response.data})
  },

methods:{
  showSubscribers(id){
    axios.get(`http://127.0.0.1:8000/api/events/${id}/subscribers`).then
    (response => {this.eventSubscribers = response.data})
    console.log(this.eventSubscribers)
}
}, 

  

}

</script>


