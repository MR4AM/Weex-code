<template>
  <div class="wrapper">
    <!-- <image :src="logo" class="logo" />
    <text class="greeting">The environment is ready6666!</text> -->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
    }
  }
}
</script>

<style scoped>
 
</style>
