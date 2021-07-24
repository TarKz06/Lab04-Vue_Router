<template>

  <p>ID : {{ event._id }}</p>
  <p>Name : {{ event.name }}</p>
  <p>Trip : {{ event.trips }}</p>
</template>

<script>
export default {
  props: ['event']
}
</script>
