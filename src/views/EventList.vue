<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <div class="pagination">
      <router-link
        id="page-prev"
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        rel="prev"
        v-if="page != 0"
      >
        Prev page
      </router-link>
      <router-link
        id="page-next"
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        rel="next"
      >
        Next page
      </router-link>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'

// import axios from 'axios'
export default {
  name: 'EventList',
  props: {
    page: {
      type: Number,
      required: true
    },
    perPage: {
      type: Number,
      required: true
    }
  },
  components: {
    EventCard // register it as a child component
  },
  data() {
    return {
      events: null,
      totalEvents: 0 // <-- Added this to store totalEvent
    }
  },
  beforeRouteEnter(routeTo, routeFrom, next) {
    EventService.getEvents(
      parseInt(routeTo.query.perPage) || 10,
      parseInt(routeTo.query.page) || 0
    )
      .then((response) => {
        next((comp) => {
          comp.events = response.data.data
          comp.totalEvents = response.headers['x-total-count']
        })
      })
      .catch(() => {
        next({ name: 'NetworkError' })
      })
  },
  beforeRouteUpdate(routeTo, routeFrom, next) {
    EventService.getEvents(
      parseInt(routeTo.query.perPage) || 10,
      parseInt(routeTo.query.page) || 0
    )
      .then((response) => {
        next((comp) => {
          comp.events = response.data.data
          comp.totalEvents = response.headers['x-total-count']
        })
      })
      .catch(() => {
        next({ name: 'NetworkError' })
      })
  },

  computed: {
    hasNextPage() {
      //fisrt , calulate total page
      let totalPages = Math.ceil(this.totalEvents / this.perPage) // 2is event per page
      //Then Check to see if the current page is less then total pages
      return this.page < totalPages
    }
  }
}
</script>
<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}
#page-prev {
  text-align: left;
}
#page-next {
  text-align: right;
}
</style>
