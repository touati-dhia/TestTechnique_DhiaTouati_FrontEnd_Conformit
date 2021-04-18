<template>
  <div :key="event.id" v-for="event in events">
    <Event
      @click="editEvent(event)"
      @toggle-solved="$emit('toggle-solved', event.id)"
      @delete-event="$emit('delete-event', event.id)"
      :event="event"
    />
  </div>
</template>

<script>
import Event from './Event'

export default {
  name: 'Events',
  props: {
    events: Array,
  },
  methods: {
    editEvent(event){
      this.$emit('event-clicked', event)
    }
  },
  components: {
    Event,
  },
  emits: ['delete-event', 'toggle-solved', 'event-clicked'],
}
</script>
