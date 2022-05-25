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

    <div class="items">
      <h1>Lista de compras</h1>
      <div class="addItemBox">
        <input v-model="itemName" placeholder="Nombre" type="text" />
        <input v-model="itemPrice" placeholder="Precio" type="text" />
        <button @click="addItem()">Añadir objeto</button>
      </div>
      <ul>
        <li class="table-title">
          <span>Producto</span>
          <span>Precio</span>
          <span>Acciones</span>
        </li>
        <li 
          v-for="item in items"
          :key="item.id">
          <span>{{ item.name }}</span>
          <span>${{ item.price }}</span>
          <div class="actions">
            <button class="edit-button" @click="editItem(item.id)">Editar</button>
            <button class="delete-button" @click="removeItem(item.id)">Eliminar</button>
          </div>
        </li>
      </ul>
    </div>
    <div class="editBox">
      <h1>Editar producto</h1>
      <div class="editItemBox">
        <input v-model="selectedItemName" placeholder="Nombre" type="text" />
        <input v-model="selectedItemPrice" placeholder="Precio" type="text" />
      </div>
  </div>
</div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      items: [],
      selectedItem: [],
      selectedItemName: "",
      selectedItemPrice: null,
      itemName: "",
      itemPrice: null,
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
        price: this.itemPrice,
      })
      this.items = [...this.items, res.data];
      this.itemName = "";
      this.itemPrice = "";
    },
    removeItem(id) {
      axios.delete(`http://localhost:3000/items/${id}`)
      this.items = this.items.filter(item => item.id !== id)
    },
    async editItem(id) {
      await axios.patch(`http://localhost:3000/items/${id}`, {
        name: this.selectedItemName,
        price: this.selectedItemPrice,
      })
      this.selectedItemName = "";
      this.selectedItemPrice = "";
    },
    async getItem(id) {
      const res = await axios.get(`http://localhost:3000/items/${id}`)
      console.log(res.data)
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
button {
  border: none;
}
.table-title {
  font-size: 1.2rem;
  font-weight: bold;
}
.actions {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(2, 50%);
  justify-content: space-evenly;
  justify-items: center;
  align-content: space-evenly;
  align-items: center;
}
.actions button {
  width: 80% !important;
}
.actions .edit-button {
  background-color: rgb(255, 239, 91);
}
.actions .delete-button {
  background-color: rgb(245, 76, 76);
  color: #fff;
}
.caja {
  width: 50%;
  margin: auto;
  background-color: #2b80ff;
  color: #fff;
  padding: 20px;
  border-radius: 20px;
}
.caja .addItemBox {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;
  justify-content: space-evenly;
  justify-items: center;
  align-content: space-evenly;
  align-items: center;
}
.caja ul {
    list-style: none;
    padding-left: 0;
    margin: 16px 0;
}
.caja ul li {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  justify-content: space-evenly;
  justify-items: center;
  align-content: space-evenly;
  align-items: center;
  margin-top: 5px;
}
.caja ul li button {
  width: 50%;
}
button {
  padding: 2px 8px;
}
</style>
