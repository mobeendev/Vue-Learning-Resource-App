<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addRes,
      deleteResourceItem: this.deleteRes,
    };
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
          userResources: ['Videos Tutorials  📹', 'Blogs 🌐', 'Books 📚'],
          choice: 'Yes 😀',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org',
          userResources: ['Books 📚', 'Blogs 🌐'],
          choice: 'No 😐',
        },
      ],
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      console.log(tab);
      this.selectedTab = tab;
    },
    deleteRes(itemId) {
      const indexOfRes = this.storedResources.findIndex(
        (item) => item.id === itemId
      );
      this.storedResources.splice(indexOfRes, 1);
    },
    addRes: function (title, description, link, userResources, choice) {
      const newResource = {
        id: crypto.randomUUID(),
        title: title,
        description: description,
        link: link,
        userResources: userResources,
        choice: choice,
      };
      console.log(title, description, link, userResources, choice);
      this.storedResources.unshift(newResource);
      console.log(this.storedResources);

      this.selectedTab = 'stored-resources';
    },
  },
};
</script>
