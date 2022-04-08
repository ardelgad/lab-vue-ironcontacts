<script>
import contacts from "./contacts.json";

export default {
  data() {
    return {
      hiddenContacts: contacts.slice(5),
      visibleContacts: contacts.slice(0, 5),
    };
  },

  methods: {
    getRandomContact() {
      // Random entre 0 y todos los contactos que quedan por mostrar
      const index = Math.floor(Math.random() * this.hiddenContacts.length);
      // Añadimos el contacto afortunado
      this.visibleContacts.push(this.hiddenContacts[index]);
      // Eliminamos el contacto de la lista de los contactos por mostrar
      this.hiddenContacts.splice(index, 1);
    },

    sortName() {
      //console.log("entro?Si");
      return this.visibleContacts.sort((c1, c2) => {if (c1.name < c2.name) {
       return -1;
      }
      });
    },

    sortPopularity() {
      //console.log("entro?Si");
      return this.visibleContacts.sort((c1, c2) => c2.popularity - c1.popularity);
    },

    removeContact(id) {
      //console.log("entro?SI");
    }
  },
};
</script>

<!-- HTML de la APP-->
<template>
  <div id="app">
    <h1>SinguContacts</h1>
    <button @click="getRandomContact()" style="margin-bottom: 15px">
      Add Contact
    </button>
    <button @click="sortPopularity()" style="margin-bottom: 15px">
      Sort by Popularity
    </button>
    <button @click="sortName()" style="margin-bottom: 15px">
      Sort by Name
    </button>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won Oscar</th>
          <th>Won Emy</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in visibleContacts" :key="contact.id">
          <td>
            <img class="photo" :src="contact.pictureUrl" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>
            <img
              v-if="contact.wonOscar"
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="oscar trophy"
            />
          </td>
          <td>
            <img
              v-if="contact.wonEmmy"
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="emmy trophy"
            />
          </td>
          <td><button @click="removeContact(contact.id)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<!-- estilos globales de la aplicación -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.photo {
  width: 100px;
}
</style>