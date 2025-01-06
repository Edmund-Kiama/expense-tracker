<template>
  <Header></Header>
  <div class="container">
    <Balance :total="total"></Balance>
    <income-expenses 
    :income="+income"
    :expenses="+expenses"
    ></income-expenses>
    <transaction-list @-transaction-deleted="handleTransactionDeleted" :transactions="transactions"></transaction-list>
    <add-transaction @transaction-submitted="handleTransactionSubmitted"></add-transaction>
  </div>
</template>

<script setup>
  import Header from './components/Header.vue'
  import Balance from './components/Balance.vue'
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';

  import { ref, computed, onMounted } from 'vue';

  const transactions = ref([]);

  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions) {
      transactions.value = savedTransactions;
    }
  })
  
  //Get total
  const total = computed (() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
  });

  //Get income
  const income = computed (() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
  }); 


  //Get expenses
  const expenses = computed (() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
  }); 

  //Add transaction 
   const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount
    });

    saveTransactionsToLocalStorage();

   };

   //Generate Unique Id
   const generateUniqueId = () => {
    return Math.floor(Math.random() * 100000);
   };

   //Delete transaction
   const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
   

    saveTransactionsToLocalStorage();
   };

   //save to local storage
   const saveTransactionsToLocalStorage = () =>{
    localStorage.setItem( 'transactions', JSON.stringify(transactions.value))
   };


</script>