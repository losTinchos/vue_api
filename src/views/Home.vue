<template>
  <div class="home">
    <h1>{{text}}</h1>
    <div class="flex flex-wrap justify-center text-red-600">

      <ul v-for="event in events" :key="event.id">
          <li @click="showSubscribers(event)" style="width: 24rem;">
            <div class="flex justify-between event-card inline-flex border-2 border-blue-dark mx-3 my-3 items-center">
            <div class="bg-blue-dark flex items-center ml-4 h-24 w-36">
                <p class="font-bold text-xl text-aqua" style="margin: auto">SQL/<br>PHP</p>
            </div>
            <div class="w-full m-2 pl-2">
                <p class="text-right">{{event.date}}</p>
                <h2 class="font-bold text-xl">{{ event.title }}</h2>
                <p class="bg-aqua-light" style="width: fit-content">{{ event.capacity }} places
                    /{{ event.remaining }} available</p>
                <p>{{ event.description }}</p>
            </div>
          </div>
        </li>
      </ul>
      <ul v-for="Subs in eventSubscribers" :key="Subs.id">
              <li @click="showSubscribers(Subs)" style="width: 24rem;"></li>
      </ul>


  </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'Home',
  components: {HelloWorld},
  data(){
    return{
      events:[],
      text:'Events',
    }
},

mounted(){
    axios.get('http://127.0.0.1:8000/api/events').then
    (response => {this.events = response.data})
    axios.get(`http://127.0.0.1:8000/api/events/8/subscribers`).then
    (response => {this.eventSubscribers = response.data})
  },
methods:{
  showSubscribers(info){
    console.log(info)

  }
}
}

</script>


