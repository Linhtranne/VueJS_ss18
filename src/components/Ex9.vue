<template>
    <div>
      <h1>Settings</h1>
      <form @submit.prevent="saveChanges">
        <div>
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="formData.username" />
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="formData.email" />
        </div>
        <button type="submit">Save</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          username: '',
          email: ''
        },
        originalData: {
          username: '',
          email: ''
        },
        isDirty: false
      };
    },
    created() {
      // Giả lập dữ liệu ban đầu (có thể thay thế bằng API call)
      this.originalData = {
        username: 'JohnDoe',
        email: 'johndoe@example.com'
      };
      this.formData = { ...this.originalData };
    },
    methods: {
      saveChanges() {

        this.originalData = { ...this.formData };
        this.isDirty = false;
        alert('Changes saved!');
      },
      checkIfDirty() {

        return (
          this.formData.username !== this.originalData.username ||
          this.formData.email !== this.originalData.email
        );
      }
    },
    watch: {
      formData: {
        handler() {

          this.isDirty = this.checkIfDirty();
        },
        deep: true
      }
    },
    beforeRouteLeave(to, from, next) {
      if (this.isDirty) {

        const answer = window.confirm(
          'Dữ liệu chưa thay đổi, bạn có muốn rời đi'
        );
        if (answer) {
          next();
        } else {
          next(false);
        }
      } else {
        next();
      }
    }
  };
  </script>
  
  <style scoped>

  form {
    max-width: 400px;
    margin: 0 auto;
  }
  button {
    margin-top: 10px;
  }
  </style>
  