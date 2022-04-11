<template>
  <!-- Highlighted class is now toggled on ternary operator and id is now iterated through with ES6+ syntax.
   -->
  <div id="numbers-container">
  <div v-for="number in numbers" :key="number.id" :class="[number.active ? 'number active' : 'number']"  @mouseover="hov(number.id)" @mouseout="hovout()" :id="`number-${number.id}`" > 
        {{number.id}}
  </div>
  </div>

</template>

<script >
export default {
    name: 'Numbers',
    // Number is now passed down as a prop

    props: [
        "numbers"
    ],
    
    emits: ["reset", "divisors"],

    // Event handlers now emit logic back to the parent component
    
    methods: {
    hov(number)
    {
        const numbers = this.numbers;
        let divisors = []

        numbers.forEach(num => {
            if(number % num.id === 0)
            {
                divisors.push(num.id);
                
            }
            
        });

        this.$emit('divisors', divisors)

    },
    hovout()
    {
        this.$emit('reset')

    },


    }
}
</script>

<style>
    .number {
        display: inline-block;
        padding: 5px;
        background-color: lightgrey;
        margin: 5px;
	}

	.active {
		background-color: red;
	}
</style>
