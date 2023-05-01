<template>
  <nav><router-link to="/login">Exit</router-link></nav>
  <router-view />
</template>

<script>
export default {
  data() {
    return {
      account1: {
        owner: "Edward",
        movements: [200, 450, -400, 3000, -650, -130, 70, 1300],
        interestRate: 1.2,
        pin: 1111,
      },
      account2: {
        owner: "Michael",
        movements: [-200, -150, -100, 3000, -650],
        interestRate: 1.2,
        pin: 2222,
      },
    };
  },
};
</script>
