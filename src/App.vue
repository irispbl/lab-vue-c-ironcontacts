// src/App.vue
<template>
  <h1>IronContacts</h1>
  <div class="botones">
    <button type="button" @click="addNewContact()">Add Random Contact</button>
    <button type="button" @click="sortPopularity()">Sort by popularity</button>
    <button type="button" @click="sortContacts()">Sort by name</button>
  </div>
  <table>
    <thead>
      <tr>
        <th>picture</th>
        <th>name</th>
        <th>popularity</th>
        <th>Won Oscar</th>
        <th>Won Emmy</th>
      </tr>

      <tr v-for="contact in contactList" :key="id">
        <td>
          <img :src="contact.pictureUrl" :alt="contact.pictureUrl" width="70" />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
        <td v-if="contact.wonOscar === true"><i class="fas fa-trophy"></i></td>
        <td v-if="contact.wonEmmy === true"><i class="fas fa-trophy"></i></td>
      </tr>
    </thead>
  </table>
</template>

<script>
import contacts from "./contacts.json";
export default {
  data() {
    return {
      contacts: contacts,
      contactList: contacts.slice(0, 5),
    };
  },
  methods: {
    addNewContact() {
      const randomContact = Math.floor(Math.random() * contacts.length);
      if (!this.contactList.includes(contacts[randomContact])) {
        this.contactList.push(contacts[randomContact]);
      }
    },
    sortContacts() {
      this.contactList.sort(function (a, b) {
        if (b.name > a.name) return -1;
        if (a.name > b.name) return 1;
      });
    },
    sortPopularity() {
      this.contactList.sort(function (a, b) {
        return b.popularity - a.popularity;
      });
    },
  },
};
</script>

<style>
h1 {
  text-align: center;
}
.botones {
  display: flex;
  justify-content: center;
}
</style>

<!--deleteElement(indice){
  contactList.splice(indice,1);
 },-->
