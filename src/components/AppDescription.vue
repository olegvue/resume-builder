<template>
  <div v-for="item in description" :key="item.id">
    <component :is="'app-' + item.type" :text="item.text"></component>
  </div>
</template>

<script>
import AppSubtitle from './AppSubtitle'
import AppText from './AppText'

export default {
  props: ['description'],
  components: {
    AppSubtitle, AppText
  }
}
</script>
