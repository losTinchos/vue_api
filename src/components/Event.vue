<template>
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
</template>

<script>
export default {
  name: 'Event',
  props: {
    event: String,
    date: Date,
    title: String,
    capacity: Number,
    description: String,
  }
}
</script>
