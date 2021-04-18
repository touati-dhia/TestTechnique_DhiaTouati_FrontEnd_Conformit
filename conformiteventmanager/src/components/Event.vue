<template>
  <div
    @dblclick="$emit('toggle-solved', event.id)"
    :class="[event.solved ? 'solved' : '', 'event']"
  >
    <h4>
      {{ event.title }}
      <i @click="$emit('delete-event', event.id)" class="fas fa-times"></i>
    </h4>
  </div>
</template>

<script>
export default {
  name: 'Event',
  props: {
    event: Object,
  },
}
</script>

<style scope>
.fas {
  color: red;
}

.event {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.event.solved {
  border-left: 5px solid green;
}

.event h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
