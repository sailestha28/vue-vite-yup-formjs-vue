<template>
  <div id="app">
    <form @submit.prevent="onSubmit" class="space-y-4 max-w-md mx-auto">
      <div>
        <label for="name" class="block text-sm font-medium text-gray-700">Name:</label>
        <input
          id="name"
          type="text"
          v-model="form.name"
     :class="[
            'mt-1 p-2 border rounded-md w-full',
            { 'border-red-500': form.errors.name }
          ]"
        />
        <span v-if="form.errors?.name" class="text-red-500 text-sm block">{{ form.errors.name }}</span>
      </div>

      <div>
        <label for="email" class="block text-sm font-medium text-gray-700">Email:</label>
        <input
          id="email"
          v-model="form.email"
       :class="[
            'mt-1 p-2 border rounded-md w-full',
            { 'border-red-500': form.errors.name }
          ]"
        />
        <span v-if="form.errors.email" class="text-red-500 text-sm block">{{ form.errors.email }}</span>
      </div>

   <button type="submit" class="w-full bg-blue-500 text-white p-2 rounded-md hover:bg-blue-600">
        Submit
      </button>
    </form>
  </div>
</template>

<script setup>
import { useForm } from "formjs-vue2";
import * as yup from "yup";

// Define the validation schema using Yup
const schema = yup.object().shape({
  name: yup.string().required("Name is required"),
  email: yup
    .string()
    .email("Enter a valid email address")
    .required("Email is required"),
});

const form = useForm({
    name: "",
    email: "",
},{schema:schema});

const onSubmit = async () => {
  const isValid = await form.validate();
  if (isValid) {
    console.log("Form submitted successfully:", form);
  } else {
    console.error("Validation errors:", errors);
  }
};
</script>

<style>
.error {
  color: red;
  font-size: 12px;
}
.is-invalid {
  border-color: red;
}
</style>
