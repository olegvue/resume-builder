<template>
  <div class="avatar" v-if="src">
    <img :src="src">
  </div>
</template>

<script>
export default {
  props: ['src']
}
</script>
