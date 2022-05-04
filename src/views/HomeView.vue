<template>
  <div class="home">
    <ViewScreen />
    <Calculator />
  </div>
</template>

<script>
// @ is an alias to /src
import Calculator from '@/components/Calculator.vue'
import ViewScreen from '@/components/ViewScreen.vue'

export default {
  name: 'HomeView',
  components: {
    Calculator,
    ViewScreen,
  }
}
</script>
