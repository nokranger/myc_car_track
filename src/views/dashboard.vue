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
        <b-button v-b-modal.modal-1>Add Data</b-button>
          <b-modal id="modal-1" title="Customer" size="xl" hide-footer>
            <b-container>
              <b-row>
                <b-col>
                  Code
                  <div>
                    <b-input v-model="customer.cus_code" ref="cus_code"></b-input>
                  </div>
                </b-col>
                <b-col>
                  Name
                  <div>
                    <b-input v-model="customer.cus_name" ref="cus_name"></b-input>
                  </div>
                </b-col>
              </b-row>
              <b-row>
                <b-col>
                  Lat
                  <div>
                    <b-input v-model="customer.lat" ref="lat"></b-input>
                  </div>
                </b-col>
                <b-col>
                  Lon
                  <div>
                    <b-input v-model="customer.lon" ref="lon"></b-input>
                  </div>
                </b-col>
                <b-col>
                  <!-- Route
                  <div>
                    <b-input v-model="customer.route_id" ref="route_id" readonly></b-input>
                  </div> -->
                </b-col>
              </b-row>
              <b-row>
                <b-col>
                  Available
                  <div>
                    <b-input v-model="customer.available" ref="available"></b-input>
                  </div>
                </b-col>
                <b-col>
                  Create At
                  <div>
                    <b-form-input type="date" v-model="customer.create_at" ref="create_at"></b-form-input>
                  </div>
                </b-col>
              </b-row>
              <br>
              <b-row>
                <b-col></b-col>
                <b-col>
                  <div>
                    <b-button v-on:click="send ()">Add data</b-button>
                  </div>
                </b-col>
                <b-col>
                </b-col>
              </b-row>
            </b-container>
        </b-modal>
      </div>
    </b-container>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      fields: ['cus_code', 'cus_name', 'lat', 'lon', 'available', 'route_id', 'create_at'],
      items: [],
      customer: [],
      code: '',
      form: {
        test: 'aaa',
        password: 'bbbb'
      }
    }
  },
  methods: {
    send () {
      console.log('send')
      console.log('ss', this.$refs.cus_code.localValue)
      this.code = this.$refs.cus_code.localValue
      axios.post('http://localhost:4000/emp/login', this.form)
        .then(response => {
          // console.log(VueJwtDecode.decode(response.data))
          // const jwt = VueJwtDecode.decode(response.data)
          // if (jwt.loginSuccessfull === true) {
          //   console.log('ss')
          //   this.error = true
          //   localStorage.setItem('username', JSON.stringify(jwt.sub))
          //   localStorage.setItem('role', JSON.stringify(jwt.role))
          //   localStorage.setItem('iat', JSON.stringify(jwt.iat))
          //   localStorage.setItem('jwt', JSON.stringify(response.data))
          //   console.log(jwt.iat)
          //   console.log(jwt.sub)
          //   location.replace('/dashboard')
          // }
        }).catch(e => {
          if (e.response.status === 404) {
            this.error = false
            this.form.user_id = ''
            this.form.password = ''
          } else if (e.response.status === 500) {
            this.error = 500
          }
        })
      // axios.post('http://localhost:4000/customer/login', this.code).then(response => {
      //   this.items = response.data.result
      //   this.customer = []
      //   this.$refs.table.refresh()
      // })
    }
  }
}
</script>

<style scoped>
</style>
