<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Detalles de Usuario
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg px-4 py-5">
          Nombre: {{ manageUser.name }}<br />
          Email: {{ manageUser.email }}<br />
          Rol: {{ manageUser.role }}<br />
          Creado el: {{ manageUser.created_at }}<br />
          Actualizado el: {{ manageUser.updated_at }}<br />
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout";

export default {
  components: {
    AppLayout,
  },

  props: {
    manageUser: Object
  },
};
</script>
