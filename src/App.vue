<template>
  <div id="App">
    <!-- limit and numbers states are now passed down as components and values passed back are done with emit -->
    <NumberInput :limit="limit" @new-limit="newLimit" />
    <Numbers :numbers="numbers" @divisors="divisors" @reset="reset" />

  </div>

</template>

<script >

  // I placed the number input within it's own component as this is best practice. the change in limit value is now emited back to the state within parent component App.vue
  import NumberInput from '@/components/NumberInput.vue';

  import Numbers from '@/components/Numbers.vue';

  export default {
  name: 'App',
  components: {NumberInput, Numbers},
  data()
  {
    return {
      limit: 100,

      //the numbers array previously created within the n() method is now within it's own state

      numbers: [],
      
    }

  },

  //since I am using the code for createNumberArray twice I thought it better to do this as a callback function

  created() {
    this.createNumbersArray()

  },

  // I placed a watcher on the state of limit so that I could rerender createNumbersArray() on change

  watch: {
    limit() {
      this.createNumbersArray()
    }
  },
  methods: {
    
    //Instead of changing the value of states in the Numbers component, it is better practice to do so in the App component

    //I placed the code for N() within a readable function name as it is better practice than algebraic
    createNumbersArray() {
      let numbers = []
      
      //Instead of manipulating the DOM directly I choose to use an active property to access which numbers should be highlighted

      for(var i = 1; i <= this.limit; i++)
      {
          numbers = [...numbers, {id: i , active: false} ];
      }
      numbers = numbers.sort(() => Math.random() - 0.5);
      this.numbers = numbers
    },
    //Since the number input is now within a child component, I used emit to access the returned value within App.vue
    newLimit(newLimit) {
      this.limit = newLimit


    },
    //divisors now prevides the logic for the hov() method within Numbers
    divisors(divisors) {

      let arr = this.numbers

      // I choose to use a forEach rather than a for loop on the divisors array as it is best practice within ES6+
      divisors.forEach(divisor => {
        const results = arr.filter((number) => number.id === divisor);

        results[0].active = true;
        
      });

    },
    reset()
    {
      //Again instead of accessing the DOM directly I changed the booleon value of all active properties back to false
      this.numbers.forEach(num => num.active = false)
    }
  }

}

</script>

<style>

</style>
