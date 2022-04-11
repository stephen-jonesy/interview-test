<template>
  <div id="number-input-container">
        <input type="number" v-model="limit" @change="onChange" :min="0" :max="1000" />
  </div>

</template>

<script >
export default {
    name: 'NumberInput',
    props: ["limit"],
 
    methods: {
        onChange() {
            
            const newLimit = this.limit
            this.$emit('new-limit', newLimit)
        }
    }
}
</script>

<style>

</style>
