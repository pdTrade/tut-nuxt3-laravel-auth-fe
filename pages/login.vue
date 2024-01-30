<script setup lang="ts">
type Credentials = {
  email: string;
  password: string;
};

const form = ref<Credentials>({
  email: '',
  password: '',
});



const handleLogin = async () => {

  let headers = {
    accept: 'application/json',
    referer: 'http://localhost:3000',
  };

  await useFetch('http://localhost:8000/sanctum/csrf-cookie', {
    headers,
    credentials: 'include',
  });

  const token = useCookie('XSRF-TOKEN');

  if (token.value) {
    headers['X-XSRF-TOKEN'] = token.value;
  }

  await useFetch('http://localhost:8000/login', {
    method: 'POST',
    headers,
    body: form.value,
    credentials: 'include',
    watch: false,
  });

  const { data } = await useFetch('http://localhost:8000/api/user', {
    headers,
    credentials: 'include',
    watch: false,
  });



}
</script>

<template>

  <div>
    page: login
  </div>

  <div class="w-full max-w-xs">
  <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="handleLogin">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
        Email
      </label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight" id="email" type="text" placeholder="xxxx@xxx.com" v-model="form.email">
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
        Password
      </label>
      <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight" id="password" type="password" placeholder="xxxxxxxx" v-model="form.password">
    </div>
    <div class="flex items-center justify-between">
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Login
      </button>
    </div>
  </form>
</div>

</template>
