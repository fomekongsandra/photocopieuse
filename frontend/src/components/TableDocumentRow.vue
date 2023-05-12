<template>
  <td>{{ document.name }}</td>
  <td class="">Control continue</td>
  <td>220ko</td>
  <td>60</td>
  <td>{{ new Date(document.createdAt).toDateString() }}</td>
  <td class="text-green-300" :style="{'color': !document.status ? 'red' : ''}">
    {{ document.status ? "Imprimee" : "En attente" }}
  </td>
  <td class="flex gap-1">
    <div v-if="user_role===Roles.ENSEIGNANT">
      <button class="text-blue-300 focus:outline-none focus:ring focus:ring-blue-300">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
             stroke="currentColor" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round"
                d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/>
        </svg>
      </button>
      <button @click="openDialog()" class="text-red-300 focus:outline-none focus:ring focus:ring-red-300">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
             stroke="currentColor" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round"
                d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
        </svg>
      </button>
    </div>

    <div>
      <button class="text-blue-300 focus:outline-none focus:ring focus:ring-blue-300" @click="download">
        <i class="fa-solid fa-download"></i>
      </button>
      <button @click="openDialog()" class="text-red-300 focus:outline-none focus:ring focus:ring-red-300">
        <i class="fa-solid fa-check"></i>
      </button>
    </div>
  </td>
</template>

<script>
import {Roles} from '@/js/roles'

export default {
  name: 'TableDocumentRow',
  data() {
    return {
      Roles: Roles
    }
  },
  props: ['document', 'user_role'],
  methods: {
    download() {
      const link = document.createElement('a');
      link.href = this.document.file;
      let extension = this.document.file.split(',')[0].split('/')[1].split(';')[0]
      link.setAttribute('download', this.document.name + '.' + extension);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};
</script>
