<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div
        class="form-control"
        :class="{ invalid: enteredTitleValidity === 'invalid' }"
      >
        <label for="title">Title</label>
        <input
          id="title"
          name="title"
          type="text"
          ref="titleInput"
          @blur="validateInput"
        />
      </div>
      <div
        class="form-control"
        :class="{ invalid: enteredDescriptionValidity === 'invalid' }"
      >
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descInput"
          @blur="validateInput"
        ></textarea>
      </div>
      <div
        class="form-control"
        :class="{ invalid: enteredUrlValidity === 'invalid' }"
      >
        <label for="link">Link</label>
        <input
          id="link"
          name="link"
          type="url"
          ref="linkInput"
          @blur="validateInput"
        />
      </div>

      <div class="form-control">
        <h4>Did you liked this form?</h4>
        <div class="choices">
          <div>
            <input
              id="interest-news"
              name="likeform"
              type="checkbox"
              value="yes"
              v-model="likeform"
            />
            <label for="like-form">Yes</label>
          </div>
          <div>
            <input
              id="interest-tutorials"
              name="likeform"
              type="checkbox"
              value="no"
              v-model="likeform"
            />
            <label for="like-form">No</label>
          </div>
        </div>
      </div>

      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
import BaseButton from './UI/BaseButton.vue';
export default {
  inject: ['addResource'],

  components: { BaseButton },
  setup() {},
  data() {
    return {
      inputIsInvalid: false,
      enteredTitleValidity: 'pending',
      enteredDescriptionValidity: 'pending',
      enteredUrlValidity: 'pending',
      likeform: [],
    };
  },
  methods: {
    validateInput() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (enteredTitle.trim() === '') {
        this.enteredTitleValidity = 'invalid';
      } else {
        this.enteredTitleValidity = 'valid';
      }

      if (enteredDescription.trim() === '') {
        this.enteredDescriptionValidity = 'invalid';
      } else {
        this.enteredDescriptionValidity = 'valid';
      }

      if (enteredUrl.trim() === '') {
        this.enteredUrlValidity = 'invalid';
      } else {
        this.enteredUrlValidity = 'valid';
      }
    },
    submitData: function () {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      } else {
        this.userNameValidity = 'valid';
      }

      this.addResource(enteredTitle, enteredDescription, enteredUrl);
    },

    confirmError: function () {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

.container {
  display: flex;
  flex-wrap: wrap;
}
.choices {
  display: flex;
  flex-wrap: wrap;
}
</style>
