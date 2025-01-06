<template>
    <h3>Add new transaction</h3>
      <form id="form" @submit.prevent="handleSubmit">
        <div class="form-control">
          <label for="text">Text</label>
          <input 
          type="text"
           id="text"
            placeholder="Enter text..." 
            v-model="text"
            />
        </div>
        <div class="form-control">
          <label for="amount"
            >Amount <br>
            ( negative - expense)<br>( positive - income)</label
          >
          <input type="text"
           id="amount" 
           placeholder="Enter amount..." 
           v-model="amount"
           />
        </div>
        <button class="btn">Add transaction</button>
      </form>
</template>

<script setup>
  import { ref } from 'vue';

  const text = ref('');
  const amount = ref('');

  const emit = defineEmits(['transactionSubmitted'])

  const handleSubmit = () => {
    if( !text.value || !amount.value){
      alert('Both Fields must be filled')
      return;
    }
    

    const transactionData = {
      text: text.value,
      amount: parseFloat(amount.value)
    }

    emit( 'transactionSubmitted', transactionData)

    text.value = '';
    amount.value ='';
  };

</script>
