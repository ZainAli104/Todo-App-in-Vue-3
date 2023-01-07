<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode='storedResButtonMode'>Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode='addResourceButtonMode'>Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResorces: [
        {
          id: 'official-guide',
          title: 'Officail Guide',
          discription: 'The official Vue.js documentation',
          link: 'http://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          discription: 'Learn to google...',
          link: 'http://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResorces,
      addResource: this.addResource,
      deleteRes: this.deleteRes,
    };
  },
  computed: {
      storedResButtonMode() {
          return this.selectedTab === 'stored-resources'? null : 'flat'
      },
      addResourceButtonMode() {
          return this.selectedTab === 'add-resource'? null : 'flat'
      }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, disc, link) {
      const newResource = {
        id: new Date().toISOString,
        title: title,
        discription: disc,
        link: link
      };
      this.storedResorces.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    deleteRes(Idres) {
      const resIndex = this.storedResorces.findIndex(res => res.id == Idres);
      this.storedResorces.splice(resIndex, 1);
    }
  },
};
</script>