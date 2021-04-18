<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Titre</label>
      <input type="text" v-model="title" name="text" placeholder="titre" />
    </div>
        <div class="form-control">
      <label>Description</label>
      <textarea v-model="description" name="desc">
         Description
      </textarea>
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="creationDate"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>

    <input type="submit" value="Save Event" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: 'AddEvent',
  data() {
    return {
      title: '',
      creationDate: '',
      solved: false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.title) {
        alert('Veuillez Ajouter un evennement')
        return
      }

      const newEvent = {
        title: this.title,
        creationDate: this.creationDate,
        solved: this.solved,
      }

      this.$emit('add-event', newEvent)

      this.title = ''
      this.creationDate = ''
      this.solved = false
    },
  },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
