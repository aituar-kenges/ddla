<template>
  <div id="new-site">
    <h3>Edit Site</h3>
    <div class="row">
    <form @submit.prevent="updateSite" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="site_id" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="name" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="dept" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="position" required>
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
    name: 'edit-site',
    data () {
      return {
        site_id: null,
        name: null,
        dept: null,
        position: null
      }
    },
    beforeRouteEnter (to, from, next) {
      db.collection('sites').where('site_id', '==', to.params.site_id).get().then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          next(vm => {
            vm.site_id = doc.data().site_id
            vm.name = doc.data().name
            vm.dept = doc.data().dept
            vm.position = doc.data().position
          })
        })
      })
    },
    watch: {
      '$route': 'fetchData'
    },
    methods: {
      fetchData () {
        db.collection('sites').where('site_id', '==', this.$route.params.site_id).get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            this.site_id = doc.data().site_id
            this.name = doc.data().name
            this.dept = doc.data().dept
            this.position = doc.data().position
          })
        })
      },
      updateSite () {
        db.collection('sites').where('site_id', '==', this.$route.params.site_id).get().then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            doc.ref.update({
              site_id: this.site_id,
              name: this.name,
              dept: this.dept,
              position: this.position
            })
            .then(() => {
              this.$router.push({ name: 'view-site', params: { site_id: this.site_id }})
            });
          })
        })
      }
    }
  }
</script>