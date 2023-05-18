<template>
  <div id="app">
    <h1 class="nama-pemilik">Yarda-motocycle</h1>
    <form @submit.prevent="addItem">
      <input v-model="newItemText" placeholder="Add Moto type">
      <button type="submit">Add</button>
    </form>
    <label>
      <input type="checkbox" v-model="hideCompleted">
      Hide sold
    </label>
    <ul>
      <li v-for="item in filteredItems" :key="item.id">
        <span :class="{ completed: item.completed }">{{ item.text }}</span>
        <button @click="completeItem(item.id)">Sold</button>
        <button @click="deleteItem(item.id)">Delete</button>
      </li>
    </ul>
    <button @click="clearCompleted" class="hapus">Remove sold</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      idCounter: 0,
      newItemText: '',
      hideCompleted: false,
    };
  },
  methods: {
    addItem() {
      const newItemText = this.newItemText.trim();

      if (newItemText) {
        this.items.push({
          id: this.idCounter++,
          text: newItemText,
          completed: false,
        });

        this.newItemText = '';
      }
    },
    completeItem(itemId) {
      const itemIndex = this.items.findIndex(item => item.id === itemId);
      this.items[itemIndex].completed = true;
    },
    deleteItem(itemId) {
      this.items = this.items.filter(item => item.id !== itemId);
    },
    clearCompleted() {
      this.items = this.items.filter(item => !item.completed);
    },
  },
  computed: {
    filteredItems() {
      return this.items.filter(item => !item.completed || !this.hideCompleted);
    },
  },
};
</script>

<style scoped>
body {
    font-family:'Times New Roman', Times, serif; color: rgba(255, 255, 255, 0.594);
    margin: 0;
    padding: 0;
    background-image: url(wp1859224-the-ninja-h2r-wallpapers.jpg);
  }
  
  #app {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  
  h1 {
    font-size: 35px;
    margin-top: 0;
  }
  
  form {
    display: flex;
    margin-bottom: 0px;
  }
  
  input[type="text"] {
    flex: 1;
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: none;
    margin-right: 10px;
  }
  
  button[type="submit"] {
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: none;
    background-color: rgba(30, 255, 0, 0.854);
    color: rgb(255, 255, 255);
    cursor: pointer;
  }
  
  label {
    margin-left: 10px;
    font-size: 16px;
  }
  
  ul {
    border-radius: 5px;
    list-style: none;
    margin: 0;
    padding: 0;
  }
  
  li {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
  }
  
  li span {
    flex: 1;
    font-size: 16px;
  }
  
  li button {
    background-color:rgba(30, 255, 0, 0.854);
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: none;
    margin-left: 5px;
    margin-right: 10px;
    cursor: pointer;
  }
  .completed {
        text-decoration: line-through;
      }
  
  #hide-completed {
    margin-left: 0px;
    cursor: pointer;
  }
  
  button[type="button"] {
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: none;
    background-color: #e74c3c;
    color: white;
    cursor: pointer;
    margin-top: 0px;
  }
  .hapus{
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: none;
    background-color: rgba(30, 255, 0, 0.854);
    color: white;
    cursor: pointer;
  }
  .nama-pemilik{
    text-align: center;
  }
</style>
