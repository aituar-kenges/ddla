<template>
  <div id="home">
    <ul class="collection with-header">
      <li class="collection-header"><h4>Sites</h4></li>
      <li v-for="site in sites" v-bind:key="site.id" class="collection-item">
        <div class="chip">{{site.dept}}</div>
        {{site.site_id}}: {{site.name}} 
         <router-link class="secondary-content" v-bind:to="{ name: 'view-site', params: { site_id: site.site_id }}"><i class="fa fa-eye"></i></router-link>
      </li>
    </ul>
    <div class="fixed-action-btn">
      <router-link to="/new" class="btn-floating btn-large red">
        <i class="fa fa-plus"></i>
      </router-link>
    </div>
  </div>
</template>

<script>
import db from './firebaseInit';
export default {
  name: 'home',
  data() {
    return {
      sites: [],
      loading: true
    };
  },
  created() {
    db
      .collection('sites')
      .orderBy('dept')
      .get()
      .then(querySnapshot => {
        this.loading = false;
        querySnapshot.forEach(doc => {
          const data = {
            id: doc.id,
            site_id: doc.data().site_id,
            name: doc.data().name,
            dept: doc.data().dept,
            position: doc.data().position
          };
          this.sites.push(data);
        });
      });
  }
};
</script>