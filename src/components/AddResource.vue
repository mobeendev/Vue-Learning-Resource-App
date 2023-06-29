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
    <div class="top-heading">
      <h2>Share your learning resources with us.</h2>
    </div>

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

      <div
        class="form-control"
        :class="{ invalid: userResourceValidity === 'invalid' }"
      >
        <h4>How do you learn?</h4>

        <div class="">
          <div class="checkbox-row">
            <input
              id="vidoes"
              name="useResource"
              type="checkbox"
              value="Vidoe Tutorials 📹"
              @blur="validateInput"
              v-model="useResource"
            />
            <label for="like-form"> Video Courses 📹</label>
          </div>
          <div class="checkbox-row">
            <input
              id="blogs"
              name="useResource"
              type="checkbox"
              value="Books 📚"
              @blur="validateInput"
              v-model="useResource"
            />
            <label for="like-form">Books 📚</label>
          </div>
          <div class="checkbox-row">
            <input
              id="blogs"
              name="useResource"
              type="checkbox"
              value="Blogs 🌐"
              @blur="validateInput"
              v-model="useResource"
            />
            <label for="like-form">Blogs 🌐</label>
          </div>
          <div class="checkbox-row">
            <input
              id="others"
              name="useResource"
              type="checkbox"
              value="Others ♾️"
              @blur="validateInput"
              v-model="useResource"
            />
            <label for="like-form">Others ♾️</label>
          </div>
        </div>
      </div>

      <div
        class="form-control"
        :class="{ invalid: userChoiceValidity === 'invalid' }"
      >
        <h4>Do you use this learning resource?</h4>
        <div class="choices">
          <div>
            <input
              id="how-video"
              name="userChoice"
              v-model="userChoice"
              type="radio"
              value="Yes 😀"
              @blur="validateInput"
            />
            <label for="how-video">Yes 😀</label>
          </div>
          <div>
            <input
              id="how-blogs"
              name="userChoice"
              v-model="userChoice"
              type="radio"
              value="No 😐"
              @blur="validateInput"
            />
            <label for="how-blogs">No 😐</label>
          </div>
          <div></div>
        </div>
      </div>
      <div style="display: flex">
        <base-button mode="right" type="submit">Add Resource</base-button>
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
      userResourceValidity: 'pending',
      useResource: [],
      userChoiceValidity: 'pending',
      userChoice: null,
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
      if (this.useResource.length === 0) {
        this.userResourceValidity = 'invalid';
      } else {
        this.userResourceValidity = 'valid';
      }

      if (this.userChoice == null) {
        this.userChoiceValidity = 'invalid';
      } else {
        this.userChoiceValidity = 'valid';
      }
    },
    submitData: function () {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;
      this.validateInput();
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
      this.addResource(
        enteredTitle,
        enteredDescription,
        enteredUrl,
        this.useResource,
        this.userChoice
      );
    },

    confirmError: function () {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
.top-heading {
  color: #a31b5f;
  display: flex;
  align-items: center;
  justify-content: center;
}
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

.checkbox-row {
  display: flex;
  align-items: baseline;
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
