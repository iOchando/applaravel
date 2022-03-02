<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Editor de Usuario
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <jet-form-section @submitted="updateProfileInformation">
          <template #title> Información del Perfil </template>

          <template #description>
            Actualice la información de perfil y la dirección de correo electrónico de la cuenta.
          </template>

          <template #form>
            <!-- Name -->
            <div class="col-span-6 sm:col-span-4">
              <jet-label for="name" value="Nombre" />
              <jet-input
                id="name"
                type="text"
                class="mt-1 block w-full"
                v-model="form.name"
                autocomplete="name"
              />
              <jet-input-error :message="form.errors.name" class="mt-2" />
            </div>

            <!-- Email -->
            <div class="col-span-6 sm:col-span-4">
              <jet-label for="email" value="Email" />
              <jet-input
                id="email"
                type="email"
                class="mt-1 block w-full"
                v-model="form.email"
              />
              <jet-input-error :message="form.errors.email" class="mt-2" />
            </div>

            <!-- Role -->
            <div
              class="col-span-6 sm:col-span-4"
              v-if="$page.props.permission.users.editRole"
            >
              <jet-label for="role" value="Rol" />
              <jet-select
                id="role"
                class="mt-1 block w-full"
                v-model="form.role"
                :options="roles"
              />
              <jet-input-error :message="form.errors.role" class="mt-2" />
            </div>
          </template>

          <template #actions>
            <jet-action-message :on="form.recentlySuccessful" class="mr-3">
              Saved.
            </jet-action-message>

            <jet-button
              :class="{ 'opacity-25': form.processing }"
              :disabled="form.processing"
            >
              Guardar
            </jet-button>
          </template>
        </jet-form-section>
      </div>
    </div>
  </app-layout>
</template>

<script>
import { useForm } from "@inertiajs/inertia-vue3";
import AppLayout from "@/Layouts/AppLayout";
import JetButton from "@/Jetstream/Button";
import JetFormSection from "@/Jetstream/FormSection";
import JetInput from "@/Jetstream/Input";
import JetInputError from "@/Jetstream/InputError";
import JetLabel from "@/Jetstream/Label";
import JetActionMessage from "@/Jetstream/ActionMessage";
import JetSecondaryButton from "@/Jetstream/SecondaryButton";
import JetSelect from "@/Components/Select";

export default {
  components: {
    AppLayout,
    JetActionMessage,
    JetButton,
    JetFormSection,
    JetInput,
    JetInputError,
    JetLabel,
    JetSecondaryButton,
    JetSelect,
  },

  props: {
    manageUser: Object,
  },

  setup(props) {
    const form = useForm({
      _method: "PUT",
      name: props.manageUser.name,
      email: props.manageUser.email,
      role: props.manageUser.role,
    });
    const roles = [
      {
        name: "Admin",
        value: "admin",
      },
      {
        name: "User",
        value: "user",
      },
    ];

    const updateProfileInformation = () => {
      form.post(route("users.update", props.manageUser.id), {
        preserveScroll: true,
      });
    };

    return { form, roles, updateProfileInformation };
  },
};
</script>
