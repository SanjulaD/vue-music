<!-- eslint-disable vuejs-accessibility/click-events-have-key-events -->
<!-- eslint-disable vuejs-accessibility/label-has-for -->
<template>
  <!-- Auth Modal -->
  <div
    class="fixed z-10 inset-0 overflow-y-auto"
    id="modal"
    :class="{ hidden: !authModelShow }"
  >
    <div
      class="
        flex
        items-end
        justify-center
        min-h-screen
        pt-4
        px-4
        pb-20
        text-center
        sm:block sm:p-0
      "
    >
      <div class="fixed inset-0 transition-opacity">
        <div class="absolute inset-0 bg-gray-800 opacity-75"></div>
      </div>

      <!-- This element is to trick the browser into centering the modal contents. -->
      <span class="hidden sm:inline-block sm:align-middle sm:h-screen"
        >&#8203;</span
      >
      <div
        class="
          inline-block
          align-bottom
          bg-white
          rounded-lg
          text-left
          overflow-hidden
          shadow-xl
          transform
          transition-all
          sm:my-8 sm:align-middle sm:max-w-lg sm:w-full
        "
      >
        <!-- Add margin if you want to see some of the overlay behind the modal-->
        <div class="py-4 text-left px-6">
          <!--Title-->
          <div class="flex justify-between items-center pb-4">
            <p class="text-2xl font-bold">Your Account</p>
            <!-- Modal Close Button -->
            <div
              class="modal-close cursor-pointer z-50"
              @click.prevent="toggleAuthModel"
            >
              <i class="fas fa-times"></i>
            </div>
          </div>

          <!-- Tabs -->
          <ul class="flex flex-wrap mb-4">
            <li class="flex-auto text-center">
              <a
                class="block rounded py-3 px-4 transition"
                href="#"
                @click.prevent="tab = 'login'"
                :class="{
                  'hover:text-white text-white bg-blue-600': tab === 'login',
                  'hover:text-blue-600': tab === 'register',
                }"
                >Login</a
              >
            </li>
            <li class="flex-auto text-center">
              <a
                class="block rounded py-3 px-4 transition"
                href="#"
                @click.prevent="tab = 'register'"
                :class="{
                  'hover:text-white text-white bg-blue-600': tab === 'register',
                  'hover:text-blue-600': tab === 'login',
                }"
                >Register</a
              >
            </li>
          </ul>

          <!-- Login Form -->
          <form v-show="tab === 'login'">
            <!-- Email -->
            <div class="mb-3">
              <label class="inline-block mb-2">Email</label>
              <input
                type="email"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Enter Email"
              />
            </div>
            <!-- Password -->
            <div class="mb-3">
              <label class="inline-block mb-2">Password</label>
              <input
                type="password"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Password"
              />
            </div>
            <button
              type="submit"
              class="
                block
                w-full
                bg-purple-600
                text-white
                py-1.5
                px-3
                rounded
                transition
                hover:bg-purple-700
              "
            >
              Submit
            </button>
          </form>
          <!-- Registration Form -->
          <VeeForm
            v-show="tab === 'register'"
            :validation-schema="schema"
           @submit="onSubmit"
          >
            <!-- Name -->
            <div class="mb-3">
              <label class="inline-block mb-2">Name</label>
              <VeeField
                name="name"
                type="text"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Enter Name"
                :rules="isRequired"
              />
              <ErrorMessage name="name" class="text-red-600" />
            </div>
            <!-- Email -->
            <div class="mb-3">
              <label class="inline-block mb-2">Email</label>
              <VeeField
                name="email"
                type="email"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Enter Email"
              />
              <ErrorMessage name="email" class="text-red-600" />
            </div>
            <!-- Age -->
            <div class="mb-3">
              <label class="inline-block mb-2">Age</label>
              <VeeField
                name="age"
                type="number"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
              />
              <ErrorMessage name="age" class="text-red-600" />
            </div>
            <!-- Password -->
            <div class="mb-3">
              <label class="inline-block mb-2">Password</label>
              <VeeField
                name="password"
                type="password"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Password"
              />
              <ErrorMessage name="password" class="text-red-600" />
            </div>
            <!-- Confirm Password -->
            <div class="mb-3">
              <label class="inline-block mb-2">Confirm Password</label>
              <VeeField
              name="confirmPassword"
                type="password"
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
                placeholder="Confirm Password"
              />
            </div>
            <!-- Country -->
            <div class="mb-3">
              <label class="inline-block mb-2">Country</label>
              <select
                class="
                  block
                  w-full
                  py-1.5
                  px-3
                  text-gray-800
                  border border-gray-300
                  transition
                  duration-500
                  focus:outline-none focus:border-black
                  rounded
                "
              >
                <option value="USA">USA</option>
                <option value="Mexico">Mexico</option>
                <option value="Germany">Germany</option>
              </select>
            </div>
            <!-- TOS -->
            <div class="mb-3 pl-6">
              <input
                type="checkbox"
                class="w-4 h-4 float-left -ml-6 mt-1 rounded"
              />
              <label class="inline-block">Accept terms of service</label>
            </div>
            <button
              class="
                block
                w-full
                bg-purple-600
                text-white
                py-1.5
                px-3
                rounded
                transition
                hover:bg-purple-700
              "
            >
              Submit
            </button>
          </VeeForm>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations, mapState } from 'vuex';
import { Field as VeeField, Form as VeeForm, ErrorMessage } from 'vee-validate';
import * as yup from 'yup';

export default {
  name: 'AuthComponent',
  data() {
    const schema = yup.object({
      email: yup.string().required().email(),
      password: yup.string().required().min(8),
      name: yup.string().required(),
      age: yup.number().required(),
    });
    return {
      tab: 'login',
      schema,
    };
  },
  components: {
    VeeField,
    VeeForm,
    ErrorMessage,
  },
  computed: {
    ...mapState(['authModelShow']),
  },
  methods: {
    ...mapMutations(['toggleAuthModel']),
    isRequired(value) {
      if (value && value.trim()) {
        return true;
      }
      return 'This is required';
    },
    onSubmit(values) {
      // Submit values to API...
      console.log(values);
    },
  },
};
</script>

<style>
</style>
