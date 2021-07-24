<template>
  <div v-if="event" class="Airline">
    <p>
      <span>
        <img :src="event.airline.logo" />
        <img
          v-if="airline in event.airline"
          :key="airline.name"
          :src="airline.logo"
        />
      </span>
    </p>
    <p>
      <span>
        <b>Airline Name :</b>
        <span>{{ event.airline.id }}</span>
        <span v-for="airline in event.airline" :key="airline.name">
          {{ airline.name }}
        </span>
      </span>
    </p>
    <p>
      <span>
        <b>ID :</b>
        <span>{{ event.airline.id }}</span>
        <span v-for="airline in event.airline" :key="airline.id">
          {{ airline.id }}
        </span>
      </span>
    </p>

    <p>
      <span>
        <b>Country:</b>
        <span>{{ event.airline.country }}</span>
        <span v-for="airline in event.airline" :key="airline.id">
          {{ airline.country }}
        </span>
      </span>
    </p>
  </div>
</template>

<script>
export default {
  props: ['event']
}
</script>
<style scoped>
.Airline {
  text-align: center;
}

img {
  width: 200px;
  height: auto;
}
</style>
