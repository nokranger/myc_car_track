<template>
  <div>
    <br>
    <h1>Dashboard</h1>
    <br>
    <b-container>
      <b-table ref="table" :items="items" :fields="fields" responsive="sm" head-variant="dark" table-variant="primary" striped bordered hover fixed outlined>
        <template v-slot:cell(first_name)="data">
          <div>
            <router-link :to="'/detail/' + data.item.first_name">
            {{data.item.first_name}}
            </router-link>
          </div>
        </template>
      </b-table>
      <br>
      <div>
        <b-button>Add Data</b-button>
      </div>
    </b-container>
  </div>
</template>
<script>
export default {
  data () {
    return {
      fields: ['first_name', 'last_name', 'age'],
      items: [
        { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        { age: 89, first_name: 'Geneva', last_name: 'Wilson' }
      ]
    }
  }
}
</script>

<style scoped>
</style>
