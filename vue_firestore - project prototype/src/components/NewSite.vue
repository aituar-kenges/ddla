<template>
  <div id="new-site">
    <h3>New Site</h3>
    <div class="row">
    <form @submit.prevent="saveSite" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="site_id" required>
          <label>Site ID#</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="name" required>
          <label>Name</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="dept" required>
          <label>Department</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="position" required>
          <label>Position</label>
        </div>
      </div>
      <button type="submit" class="btn">Submit</button>
      <router-link to="/" class="btn grey">Cancel</router-link>
    </form>
  </div>
  </div>
</template>

<script>
    import db from './firebaseInit'
    export default {
      name: 'new-site',
      data () {
        return {
          site_id: null,
          name: null,
          dept: null,
          position: null
        }
      },
      methods: {
        saveSite () {
          db.collection('sites').add({
            site_id: this.site_id,
            name: this.name,
            dept: this.dept,
            position: this.position
          })
          .then(docRef => {
            console.log('Client added: ', docRef.id)
            this.$router.push('/')
          })
          .catch(error => {
            console.error('Error adding site: ', error)
          })
        }
      }
    }
</script>
