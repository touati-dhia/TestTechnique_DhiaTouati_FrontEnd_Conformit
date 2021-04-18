<template>
  <AddEvent v-show="showAddEvent" @add-event="addEvent" @edit-event= "editEvent" />
  <Events
    @toggle-solved="toggleReminder"
    @delete-event="deleteEvent"
    :events="events"
    @event-clicked="clickedEvent"
  />
</template>

<script>
import Events from '../components/Events'
import AddEvent from '../components/AddEvent'
export default {
  name: 'Home',
  props: {
    showAddEvent: Boolean,
  },
  components: {
    Events,
    AddEvent,
  },
  data() {
    return {
      events: [],
    }
  },
  methods: {
    clickedEvent(event){
      AddEvent.event = event
    },
    async addEvent(event) {
      const res = await fetch('api/events', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(event),
      })

      const data = await res.json()

      this.events = [...this.events, data]
    },
     async editEvent(event) {
      const res = await fetch(`api/events/${event.id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(event),
      })

      const data = await res.json()

      this.events = [...this.events, data]
    },
    async deleteEvent(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/events/${id}`, {
          method: 'DELETE',
        })

        res.status === 200
          ? (this.events = this.events.filter((event) => event.id !== id))
          : alert('Error deleting event')
      }
    },
    async toggleReminder(id) {
      const eventToToggle = await this.fetchEvent(id)
      const updEvent = { ...eventToToggle, solved: !eventToToggle.solved }

      const res = await fetch(`api/events/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updEvent),
      })

      const data = await res.json()

      this.events = this.events.map((event) =>
        event.id === id ? { ...event, solved: data.solved } : event
      )
    },
    async fetchEvents() {
      const res = await fetch('api/events')

      const data = await res.json()

      return data
    },
    async fetchEvent(id) {
      const res = await fetch(`api/events/${id}`)

      const data = await res.json()

      return data
    },
    async fetchEmployees(){
      const res = await fetch('api/employees')

      const data = await res.json()

      return data
    },
  },
  async created() {
    this.events = await this.fetchEvents()
  },
}
</script>
