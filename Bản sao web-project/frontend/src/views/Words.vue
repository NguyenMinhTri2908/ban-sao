<template>
    <div>
      <h1>Words List</h1>
      <table class="ui celled table">
        <thead>
          <tr>
            <th>Word</th>
            <th>Meaning</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="word in words" :key="word._id">
            <td>{{ word.word }}</td>
            <td>{{ word.meaning }}</td>
            <td>
              
              <router-link 
                :to="{ name: 'show', params: { id: word._id } }" 
                class="ui mini button blue"
              >
                View
              </router-link>
              <router-link 
                :to="{ name: 'edit', params: { id: word._id } }" 
                class="ui mini button orange"
              >
                Edit
              </router-link>
              <button @click="deleteWord(word._id)" class="ui mini button red">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import Swal from 'sweetalert2';
  
  export default {
    name: 'Words',
    data() {
      return {
        words: []
      };
    },
    methods: {
      async getWords() {
        try {
          const response = await axios.get('http://localhost:5001/api/words');
          this.words = response.data;
        } catch (error) {
          console.error(error);
          Swal.fire('Error', 'Failed to load words', 'error');
        }
      },
      async deleteWord(id) {
        const confirm = await Swal.fire({
          title: 'Are you sure?',
          text: "You won't be able to revert this!",
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#d33',
          cancelButtonColor: '#3085d6',
          confirmButtonText: 'Yes, delete it!'
        });
  
        if (confirm.isConfirmed) {
          try {
            await axios.delete(`http://localhost:5001/api/words/${id}`);
            Swal.fire('Deleted!', 'Your word has been deleted.', 'success');
            this.getWords();
          } catch (error) {
            console.error(error);
            Swal.fire('Error', 'Failed to delete word', 'error');
          }
        }
      }
    },
    mounted() {
      this.getWords();
    }
  };
  </script>
  
  <style scoped>
  h1 {
    margin-bottom: 20px;
  }
  </style>