<template>
  <nav class="navbar navbar-expand-lg navbar-light" style="background-color: orange">
    <img src="../assets/shop-logo.png" width="50px" height="50px" class="navbar-brand mr-5" alt="Ecommerce-Logo">
    <div class="collapse navbar-collapse row justify-content-between" id="navbarSupportedContent">
      <div class="row justify-content-space">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <router-link class="nav-link mr-5" to="/">Home</router-link>
          </li>
        </ul>
      </div>
      <div class="row justify-content-end pr-5">
        <div class="nav-item mr-5">
          <div v-if="cartsCount === 0" class="numberCircle ml-4" style="margin-top: -5px; color: red">{{cartsCount}}</div>
          <div v-else class="numberCircle ml-4" style="margin-top: -5px; color: green">{{cartsCount}}</div>
          <router-link to="/cart"><i class="fas fa-cart-plus mt-1" style="color: white; font-size: 30px"></i></router-link>
        </div>
        <div>
          <button type="button" class="btn btn-outline-info dropdown-toggle" data-toggle="dropdown" aria-haspopup="true"
            aria-expanded="false">
            Profile
          </button>
          <div class="dropdown-menu dropdown-menu-right">
            <a class="dropdown-item" style="cursor: pointer;">{{getName}}</a>
            <router-link to="/history" class="dropdown-item">History</router-link>
            <a class="dropdown-item" style="cursor: pointer;" @click="logout">Logout</a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'EcommerceNavbar',
  data () {
    return {
      search: ''
    }
  },
  methods: {
    logout () {
      localStorage.clear()
      this.$store.commit('SET_CART_ID', 0)
      this.$store.commit('SET_LOGIN', false)
      this.$router.push('/login')
      this.$toasted.success('Thanks for Coming')
    }
  },
  computed: {
    email () {
      return this.$store.state.email
    },
    getName () {
      return this.email.substr(0, this.email.indexOf('@'))
    },
    cartsCount () {
      return this.$store.state.carts.length
    }
  },
  created () {
    this.$store.dispatch('fetchCart')
  }
}

</script>

<style scoped>
.numberCircle {
  position: fixed;
  font: 18px Arial, sans-serif;
  font-weight: bold;
}
</style>
