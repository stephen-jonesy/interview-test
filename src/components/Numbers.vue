<template>
  <div id="numbers-container">
  <div v-for="number in numbers" :key="number.id" :class="[number.active ? 'number active' : 'number']"  @mouseover="hov(number.id)" @mouseout="hovout()" :id="`number-${number.id}`" > 
        {{number.id}}
  </div>
  </div>

</template>

<script >
export default {
    name: 'Numbers',
    props: [
        "numbers"
    ],
    emits: ["reset", "divisors"],
    
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
    eventHandler(event) {
        console.log(event.target.id)
    }

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
