<template>
  <img :src="`/icons/${icon}.svg`" alt="">
</template>

<script>
export default {
  name: 'Icon',
  props: {
    icon: String
  }
}
</script>