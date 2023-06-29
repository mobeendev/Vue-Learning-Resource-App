<template>
  <base-card>
    <li>
      <div>
        <header>
          <h3>{{ title }}</h3>
          <base-button
            ref="resItem"
            id="itemId"
            @click="deleteResource(itemId)"
          >
            Delete
          </base-button>
        </header>
      </div>
      <p>{{ description }}</p>
      <p>Is this resource used by the Author - {{ userChoice }}</p>
      <p>Authors mode of learning -</p>
      <ul>
        <li v-for="userRes in resourcesList">{{ userRes }}</li>
      </ul>
      <nav>
        <a :href="link">View Resource</a>
      </nav>
    </li>
  </base-card>
</template>

<script>
export default {
  props: [
    'title',
    'description',
    'link',
    'itemId',
    'resourcesList',
    'userChoice',
  ],
  inject: ['deleteResourceItem'],
  methods: {
    deleteResource(itemId) {
      this.deleteResourceItem(itemId);
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
ul {
  margin-top: 1rem;
  margin: auto;
  margin-bottom: 0.3rem;
  font-size: 15px;
}
</style>
