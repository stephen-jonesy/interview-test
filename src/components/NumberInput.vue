<template>
  <!-- Capped min and max interation on input buttons -->
  <div id="number-input-container">
        <input type="number" id="number-input" v-model="changedLimit" @change="onChangeHandler" :min="0" :max="10000" />
  </div>

</template>

<script >
export default {
    name: 'NumberInput',
    // limit is now passed down as a prop

    props: ["limit"],
    data()
    {
        return {

        // The state should not be mutated within a child component, so I created a local state for limit
        
        changedLimit: this.limit,
        numbers: [],
        
        }

    },

    methods: {
        onChangeHandler() {

            // As the application has proformance issues after limit reaching 10,000, I choose to cap its manual output at 10,000

            if (this.changedLimit > 10000) {
                this.changedLimit = 10000
                let newLimit = this.changedLimit

                this.$emit('new-limit', newLimit)

            }
            else {
                let newLimit = this.changedLimit
                this.$emit('new-limit', newLimit)

            }

        }
    }
}
</script>

<style scoped>
    /* styled #number-input width with a scoped component*/
    #number-input {
        width: 100px;
    }


</style>
