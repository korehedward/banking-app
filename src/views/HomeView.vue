<template>
  <body class="h-screen bg-slate-200 flex flex-col">
    <div class="flex items-center text-center text-3xl space-x-4">
      <img src="../assets/logo.png" alt="logo" />
      <h1>Welcome back, {{ account.owner }}</h1>
    </div>
    <header
      class="flex justify-around text-4xl mt-16 w-screen space-x-96 mb-4 mr-9 font-semibold text-gray-700"
    >
      <div>
        <h1>Current balance</h1>
        <p class="text-xl mt-2 mb-4">As of: {{ displayDate() }}</p>
      </div>
      <div>${{ calculateBalance() }}</div>
    </header>
    <main class="flex space-x-6 justify-center items-center h-96">
      <div class="ml-4 w-6/12 overflow-y-scroll bg-slate-100 p-4 rounded-xl">
        <ul class="h-96 text-xl">
          <li v-for="(mov, index) in account.movements" class="mb-2">
            <div class="flex items-center text-right justify-between">
              <div>
                <p
                  v-if="mov >= 0"
                  class="bg-gradient-to-b from-green-300 to-green-400 w-40 text-center rounded-lg text-green-600"
                >
                  Deposit
                </p>
                <p
                  v-if="mov < 0"
                  class="bg-gradient-to-b from-red-300 to-red-400 w-40 text-center rounded-lg text-red-600"
                >
                  Withdrawal
                </p>
              </div>
              <div>
                <p>{{ mov }}$</p>
              </div>
            </div>
            <div class="h-px w-full bg-gray-200 mt-px"></div>
          </li>
        </ul>
      </div>
      <div class="space-y-8 w-96">
        <div
          class="flex bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 h-48 p-2 rounded-lg text-xl flex-col items-center shadow-lg shadow-purple-600"
        >
          <h2 class="mb-1 text-white">Transfer money</h2>
          <form class="flex flex-col space-y-4 items-center">
            <input
              type="text"
              placeholder="Transfer to"
              class="bg-purple-300 rounded-md pl-2"
            />
            <input
              type="number"
              placeholder="Amount"
              v-model="transferAmount"
              class="bg-purple-300 rounded-md pl-2 text-black"
            />
            <button
              class="bg-purple-300 w-32 justify-center rounded-xl text-purple-700"
              @click.prevent="transferMoney"
            >
              Send
            </button>
          </form>
        </div>
        <div
          class="flex flex-col items-center space-y-4 text-xl h-48 bg-gradient-to-r from-indigo-500 from-10% via-sky-500 via-30% to-emerald-500 to-90% h-40 p-4 rounded-lg shadow-lg shadow-cyan-600"
        >
          <h2 class="mb-1 text-white">Request loan</h2>
          <form class="space-x-4 flex-col flex items-center">
            <input
              class="bg-cyan-300 rounded-md pl-2"
              type="number"
              v-model="loanAmount"
              placeholder="Amount"
            />
            <button
              class="bg-cyan-300 w-32 mt-4 rounded-xl text-cyan-700"
              @click.prevent="loanMoney"
            >
              Request
            </button>
          </form>
        </div>
      </div>
    </main>
    <footer class="flex mt-8 justify-stretch w-screen text-2xl space-x-4 pl-96">
      <div class="text-green-400 font-thin bg-white p-1 rounded-xl">
        Income: ${{ calculateIncome() }}
      </div>
      <div class="text-red-400 font-thin bg-white p-1 rounded-xl">
        Outgoing: ${{ calculateOutgoing() }}
      </div>
    </footer>
  </body>
</template>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      currentBalance: null,
      transferAmount: null,
      loanAmount: null,
      account: {
        owner: "Edward",
        movements: [200, 450, -400, 3000, -650, -130, 70, 1300],
        interestRate: 1.2,
        pin: 1111,
      },
    };
  },
  methods: {
    displayDate() {
      const currentDate = new Date(Date.now());
      return currentDate.toDateString();
    },

    calculateBalance() {
      const balance = this.account.movements.reduce(
        (accumulator, currentValue) => {
          return accumulator + currentValue;
        },
        0
      );
      this.currentBalance = balance;
      return balance;
    },
    calculateIncome() {
      const income = this.account.movements
        .filter((mov) => mov > 0)
        .reduce((acc, mov) => {
          return (acc += mov);
        }, 0);
      return income;
    },
    calculateOutgoing() {
      const outgoing = this.account.movements
        .filter((mov) => mov < 0)
        .reduce((acc, mov) => {
          return (acc += mov);
        }, 0);
      return outgoing;
    },

    transferMoney() {
      if (this.transferAmount > this.currentBalance) {
        alert("You do not have sufficient funds to perform this task!");
      } else {
        this.account.movements.unshift(-this.transferAmount);
      }
    },
    loanMoney() {
      this.account.movements.unshift(this.loanAmount);
    },
  },
};
</script>
