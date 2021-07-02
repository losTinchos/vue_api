<template>
  <ul class="flex flex-wrap justify-center">
     <div v-for="subscribers in eventSubscribers" :key="subscribers">{{subscribers.name}}</div>
          <div :key="event.id" style="width: 24rem;">
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
</template>

<script>
import axios from 'axios'
export default {
    name: 'Event',
    eventSubscribers: [],
    props: 
    [
    "event",
    "date",
    "title",
    "capacity",
    "description"
    ],

  methods:{
  showSubscribers(id){
    axios.get(`http://127.0.0.1:8000/api/events/${id}/subscribers`).then
    (response => {this.eventSubscribers = response.data})
    console.log(this.eventSubscribers)
}
}, 
    
}
</script>
