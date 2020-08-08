<template>
  <div>
    <label for>Choose a Country</label>
    <select name="countries" id="countries" v-model="countries">
      <option value="country">{{ country }}</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      countries: []
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
