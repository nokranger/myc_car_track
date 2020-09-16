<template>
  <div>
    <br>
    Detail - {{name}}
    <br>
    <!-- {{items}} -->
    <div v-for="(item, index) in items" :key="index">
      <b-container>
        <b-row>
          <b-col>
            Code
            <div>
              <b-input v-model="item.cus_code" readonly></b-input>
            </div>
          </b-col>
          <b-col>
            Name
            <div>
              <b-input v-model="item.cus_name" readonly></b-input>
            </div>
          </b-col>
          <b-col></b-col>
        </b-row>
        <br>
        <b-row>
          <b-col>
            Lat
            <div>
              <b-input v-model="item.lat" readonly></b-input>
            </div>
          </b-col>
          <b-col>
            Lon
            <div>
              <b-input v-model="item.lon" readonly></b-input>
            </div>
          </b-col>
          <b-col>
            Route
            <div>
              <b-input v-model="item.route_id"></b-input>
            </div>
          </b-col>
        </b-row>
        <br>
        <b-row>
          <b-col>
            Available
            <div>
              <b-input v-model="item.available" readonly></b-input>
            </div>
          </b-col>
          <b-col></b-col>
          <b-col></b-col>
        </b-row>
        <br>
        <b-row>
          <b-col>
            Create At
            <div>
              <b-input ref="start_date" v-model="item.create_at" readonly></b-input>
            </div>
          </b-col>
          <b-col>
            Upate At
            <div>
              <b-input type="date" v-model="item.update_at"></b-input>
            </div>
          </b-col>
          <b-col>
            <!-- Delete At
            <div>
              <b-input v-model="item.delete_at"></b-input>
            </div> -->
          </b-col>
        </b-row>
        <br>
        <b-button variant="success" v-on:click="updateDetail ()">Upadte</b-button>
      </b-container>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      name: '',
      form: {
        name
      },
      items: [],
      updates: {
        cus_code: '',
        route_id: '',
        update_at: ''
      }
    }
  },
  beforeCreate () {},
  created () {},
  beforeUpdate () {},
  mounted () {
    console.log(this.$route.params.name)
    this.name = this.$route.params.name
    this.form.name = this.name
    axios.post('http://localhost:4000/customer/getdetail', this.form).then(response => {
      this.items = response.data.result
    })
  },
  methods: {
    updateDetail () {
      this.updates.route_id = this.items[0].route_id
      this.updates.cus_code = this.items[0].cus_code
      this.updates.update_at = this.items[0].update_at
      axios.patch('http://localhost:4000/customer/updatedetail', this.updates).then(response => {
        console.log('update')
        this.items = response.data.result
      })
    }
  },
  metaInfo () {
    return {
      title: 'Detail',
      titleTemplate: '%s - MYC'
    }
  }
}
</script>

<style scoped>
</style>
