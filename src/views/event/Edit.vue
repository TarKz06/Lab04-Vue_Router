<template>
  <p>Edit the event here</p>
  <button @click="edit">Edit</button>
</template>

<script>
export default {
  props: ['event'],
  inject: ['GStore'], //<---- Inject the glebal Store
  methods: {
    edit() {
      this.$router.push({
        name: 'EventList',
        params: { id: this.event._id }
      }),
        (this.GStore.flashMessage =
          'You are successfully updated for ' + this.event.name)
      setTimeout(() => {
        this.GStore.flashMessage = ''
      }, 3000)
    }
  }
}
</script>
