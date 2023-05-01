<template>
  <body
    class="bg-[conic-gradient(at_bottom_left,_var(--tw-gradient-stops))] from-fuchsia-300 via-green-400 to-rose-700"
  >
    <div class="h-screen w-96 ml-auto mr-auto flex items-center">
      <nav
        class="flex flex-col items-center h-3/6 w-96 rounded-xl bg-gradient-to-r from-purple-200 to-cyan-200 text-white shadow-xl"
      >
        <p class="text-3xl mt-8 text-blue-800">Log in to get started</p>
        <form class="space-y-8 mt-16 flex-col flex items-center">
          <input
            class="w-72 h-10 rounded-md pl-4"
            type="text"
            placeholder="USER"
          />
          <input
            class="w-72 h-10 rounded-md pl-4"
            type="password"
            placeholder="PIN"
            maxlength="4"
          />
          <router-link
            to="/"
            class="text-2xl w-32 text-center rounded-md bg-gradient-to-r from-cyan-500 to-blue-500 font-semibold h-10 pt-1 shadow-md"
            >Log in</router-link
          >
        </form>
      </nav>
    </div>
  </body>
</template>

<script>
export default {};
</script>
