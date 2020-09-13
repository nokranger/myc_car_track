<template>
  <div>
    <br>
    Detail - {{name}}
    <b-container>
    </b-container>
  </div>
</template>
<script>
export default {
  data () {
    return {
      name: ''
    }
  },
  beforeCreate () {},
  created () {},
  beforeUpdate () {},
  mounted () {
    console.log(this.$route.params.name)
    this.name = this.$route.params.name
  }
}
</script>

<style scoped>
</style>
