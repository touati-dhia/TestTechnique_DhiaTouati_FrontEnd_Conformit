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
      <label>Date</label>
      <input
        type="date"
        v-model="creationDate"
        name="day"
        placeholder="date"
      />
      </div>
      <div class="form-control">
      <label>Heure</label>
      <input
        type="time"
        v-model="creationHour"
        name="time"
        placeholder="heure"
      />
      </div>
      <div class="form-control">
      <label>Nom du status</label>
      <select id="status" name="status" v-model="statusName">
        <option value="Open">ouvert</option>
        <option value="InProgress">En cours</option>
        <option value="Closed">Terminé</option>
      </select> 
      </div>
      <div class="form-control">
      <label>Employé Impliqué</label>
      <select id="emp" name="emp" v-model="involvedEmployeeId">
        <option value="" disabled selected hidden>Employé</option>
      </select> 
      </div>
      <div class="form-control">
      <label>Témoins</label>
      <textarea v-model="Temoins" name="temoins">
         Témoins
      </textarea>
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
      createdBy: '',
      involvedEmployeeId: '',
      description: '',
      statusName: '',
      Temoins: '',
    }
  },
  props:{
    event: Object
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
        createdBy: 'dhia touati',
        involvedEmployeeId: this.involvedEmployeeId,
        description: this.description,
        statusName: this.statusName,
        Temoins: this.Temoins,
      }
    if (!this.event)
    {
      this.$emit('add-event', newEvent)
    }
    else{
      this.$emit('edit-event', newEvent)
    }
      
      this.title = ''
      this.creationDate = ''
      this.involvedEmployeeId  = '' 
      this.description = ''
      this.statusName = ''
      this.Temoins = ''
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
