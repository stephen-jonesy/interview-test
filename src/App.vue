<template>
  <div id="App">
    <NumberInput :limit="limit" @new-limit="newLimit" />
    <Numbers :numbers="numbers" @divisors="divisors" @reset="reset" />

  </div>

</template>

<script >
  import NumberInput from '@/components/NumberInput.vue';
  import Numbers from '@/components/Numbers.vue';

  export default {
  name: 'App',
  components: {NumberInput, Numbers},
  data()
  {
    return {
      limit: 100,
      numbers: [],
      
    }

  },
  created() {
    this.createNumbersArray()

  },
  watch: {
    limit(newVal, oldVal) {
      this.createNumbersArray()
    }
  },
  methods: {
    createNumbersArray() {
      let numbers = []
      for(var i = 1; i <= this.limit; i++)
      {
          numbers = [...numbers, {id: i , active: false} ];
      }
      numbers = numbers.sort(() => Math.random() - 0.5);
      this.numbers = numbers
    },
    newLimit(newLimit) {
      if (newLimit > 10000) {
          this.limit = 10000

      }
      else {
        this.limit = newLimit

      }

    },
    divisors(divisors) {

      let arr = this.numbers

      divisors.forEach(divisor => {
        const results = arr.filter((number) => number.id === divisor);

        results[0].active = true;
        
      });

    },
    reset()
    {
      this.numbers.forEach(num => num.active = false)
    }
  }

}

</script>

<style>

</style>
