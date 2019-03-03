<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">Test Scg</b-navbar-brand>

        <b-navbar-toggle target="nav_collapse"/>

        <b-collapse is-nav id="nav_collapse">
          <b-navbar-nav>
            <b-nav-item href="#">Function find X</b-nav-item>
            <b-nav-item href="#">Api Place Search</b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <b-form-input size="sm" class="mr-sm-2" type="text" placeholder="Search"/>
              <b-button size="sm" class="my-2 my-sm-0">Search</b-button>
            </b-nav-form>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>
    <div class="row">
      <div class="col-6">
        <b-card title="Find X">
          <b-card-text>3, 5, 9, 15, X Press button below to find X</b-card-text>
          <b-card-text>X value is {{dataX}}</b-card-text>
          <b-button variant="primary" @click.prevent="getXvalue">Find X</b-button>
        </b-card>
      </div>
      <div class="col-6">
        <b-card title="Call api">
          <b-card-text>test to call api</b-card-text>
          <input type="text" class="form-control" id="dataSearch" v-model="dataSearch" >
          <b-card-text>data ::  {{apiValue}}</b-card-text>
          <b-button variant="primary" @click.prevent="getApi">call api</b-button>
        </b-card>
      </div>
    </div>
    <div class="footer" toggleable="lg" type="dark" variant="info">
      <p>Footer</p>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      dataX: '???',
      value: [3, 5, 9, 15],
      apiValue: '',
      dataSearch: ''
    }
  },
  methods: {
    getXvalue () {
      var x = 0
      for (let i = 0; i < 4; i++) {
        if (i !== this.value.length - 1) {
          x = this.value[i + 1] - this.value[i] + 2
        } else {
          this.dataX = x + this.value[i]
        }
        console.log(this.value[i])
        console.log(this.dataX)
      }
    },
    getApi () {
      console.log('test')
      Axios.get('https://api.github.com/search/users?q=' + this.dataSearch)
        .then(({data}) => {
          console.log(JSON.stringify(data))
          this.apiValue = JSON.stringify(data)
        }).catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: #17a2b8;
  color: white;
  text-align: center;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
</style>
