<template>
  <div class="caja">
    <!-- 
            Metodo GET

    <h1>Lista de compras</h1>
    <ul>
      <li v-for="item in items" :key="item.id">
        {{ item.name }}
      </li>
    </ul> -->

    <h1>Lista de compras</h1>
    <input v-model="itemName" @keyup.enter="addItem" type="text" /><br />
    <button @click="addItem()">Añadir objeto</button>
    <ul>
      <li 
        v-for="item in items" 
        :key="item.id"
        @click="removeItem(item.id)">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      items: [],
      itemName: "",
    };
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/items`)
      this.items = res.data;
    } catch (error) {
      console.log(error)
    }
  },
  methods: {
    async addItem() {
      const res = await axios.post(`http://localhost:3000/items`, {
        name: this.itemName,
      })
      this.items = [...this.items, res.data];
      this.itemName = "";
    },
    removeItem(id) {
      axios.delete(`http://localhost:3000/items/${id}`)
      this.items = this.items.filter(item => item.id !== id)
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.caja {
  width: 25%;
  height: 25%;
  margin: auto;
  background-color: #2c0074;
  color: #fff;
}
.caja ul {
    list-style: none;
    padding-left: 0;
}
</style>
