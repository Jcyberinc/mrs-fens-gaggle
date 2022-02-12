<template>
  <div class="home">
    <h1>Mrs. Fens' Gaggle</h1>
    <Goose name="Huey" />
  </div>
</template>

<script>
import Goose from '@/components/Goose.vue'

export default {
  name: 'Home',
  components: {
    Goose
  }
}
</script>
