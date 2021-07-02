<template>
  <div class="home">
    <h1>{{text}}</h1>
    <div class="flex flex-wrap justify-center text-red-600">
      <!--<Event v-for="event in events" :key="event.id" :event="event" :date="event.date"
    :title="event.title" :capacity="event.capacity" :description="event.description" 
    :method="event.showSubscribers" /> -->
      <div class="text-green-600" v-for="subscribers in eventSubscribers" :key="subscribers">{{subscribers.name}}</div>
       <ul class="flex flex-wrap justify-center">
          <div v-for="event in events" :key="event.id" style="width: 24rem;">
            <div class="flex justify-between event-card inline-flex border-2 border-blue-dark mx-3 my-3 items-center">
            <div class="bg-blue-dark flex items-center ml-4 h-24 w-36">
                <p class="font-bold text-xl text-aqua" style="margin: auto">SQL/<br>PHP</p>
            </div>
            <div class="w-full m-2 pl-2">
                <p class="text-right">{{event.date}}</p>
                <h2 class="font-bold text-xl">{{ event.title }}</h2>
                <p class="bg-aqua-light" style="width: fit-content">{{ event.capacity }} places
                    /{{ event.capacity }} available</p>
                <p>{{ event.description }}</p>
                  <button @click="showSubscribers(event.id)" class="text-blue-600 font-bold">Subscribers</button>
            </div>
          </div>
        </div>
      </ul>
   

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


