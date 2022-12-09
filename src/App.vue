// src/App.vue
<template>
  <h1>IronContacts</h1>
  <button type="button" @click="addNewContact()"> Add Random Contact</button>
  <button type="button">Sort by popularity</button>
  <button type="button" @click="sortContacts()">Sort by name</button>
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
        <td><img :src="contact.pictureUrl" :alt="contact.pictureUrl" width="70"/></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
        <td v-if="contact.wonOscar===true"> <i class="fas fa-trophy"></i></td>
        <td v-if="contact.wonEmmy ===true"> <i class="fas fa-trophy"></i></td>
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
      contactList: contacts.slice(0,5),
    };
  },
  methods: {
    addNewContact (){
    const randomContact = Math.floor(Math.random() * contacts.length);
    if(!this.contactList.includes(contacts[randomContact])){
      this.contactList.push(contacts[randomContact]);
    }
   },
   sortContacts(){
    this.contactList.sort(function (a,b){
      if (b > a){
        return -1;
      } if (a > b){
        return 1;
      }
      return 0;
    })
   }
  },
};
</script>

<style></style>

<!--deleteElement(indice){
  contactList.splice(indice,1);
 },-->