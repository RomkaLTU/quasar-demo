<template>
  <q-page class="flex flex-center">
    <div class="container">
      <div class="row q-col-gutter-x-xs q-col-gutter-y-lg">
        <div class="col-6 col-md-4 col-lg-3" v-for="(shop,index) in $store.getters['shops/getShops']" :key="`md-${index}`">
          <div class="flex-item bg-red-5 text-white cursor-pointer" @click="showDetails(shop)">
            {{ shop.name }}
          </div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',

  mounted () {
    this.fetshShops()
  },

  methods: {
    fetshShops () {
      this.$axios.get('https://demoapi.thedenstore.com/api/service?Request=Stores&Language=en-us').then((response) => this.$store.commit('shops/setShops', response.data))
    },
    showDetails (shop) {
      this.$q.dialog({
        title: shop.name,
        message: 'Some HTML goes here...',
        html: true
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.flex-item {
  padding: 1rem;
  min-height: 90px;
}
</style>
