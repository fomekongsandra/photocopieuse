<template lang="html">
  <div class="mx-12">
    <div class="overlay-dialog transition ease-in-out delay-150 -translate-y-1 hover:scale-110 duration-300"
         v-if="dialog" @click="closeDialog">
      <div class="bg-white flex items-center justify-center p-8 rounded-md modal-dialog ">
        <div>
          <p class="text-center"><i class="fa-solid fa-circle-exclamation text-red-400 fa-2x"></i></p>
          <h2 class="text-2xl">Voulez vous vraiment Supprimer</h2>
          <div class="flex justify-center py-4 gap-8 text-white">
            <button
                class="bg-blue-500 rounded-sm px-4 py-2 focus:outline-none focus:ring focus:ring-r-300 focus:ring-opacity-80"
                @click="closeDialog">Annuler
            </button>
            <button
                class="px-4 py-2 rounded-sm bg-red-500 focus:outline-none focus:ring focus:ring-red-300 focus:ring-opacity-80"
                @click="closeDialog">Supprimer
            </button>
          </div>
        </div>
      </div>
    </div>
    <h2 class="text-2xl">Liste de fichiers importees</h2>
    <div class="d-content my-16 p-5 rounded-md">
      <table class="bg-white rounded-md">
        <thead>
        <tr>
          <th class="border-collapse">Intitule</th>
          <th class="">Type document</th>
          <th>Taille document</th>
          <th>Nombre de photocopie</th>
          <th>Date ajout</th>
          <th>Etat</th>
          <th>Actions</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="document in user?.documents" :key="document._id">
          <table-document-row :document="document" :usr_role="user_role"/>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import TableDocumentRow from "@/components/TableDocumentRow";

export default {
  components:{
    TableDocumentRow
  },
  props: ['user'],
  data: function () {
    return {
      dialog: false,
      user_role: this.user.role
    }
  },
  methods: {
    openDialog: function () {
      this.dialog = true
    },
     closeDialog: async function () {
      this.dialog = false
       await axios.delete("http://localhost/document/")
    }
  }
}
</script>
<style lang="css">
.modal-dialog {
  max-width: 500px;
  height: 200px;
}

.overlay-dialog {
  z-index: 5;
  position: fixed;
  top: 0%;
  left: 0%;
  right: 0%;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background: rgba(80, 81, 82, 0.342);
  transition: .5s all ease-in-out;
  animation: cubic-bezier(0.075, 0.82, 0.165, 1);
}
</style>