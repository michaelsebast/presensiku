<template>
  <div>
    <p>Hi from {{ name }}</p>
    <NuxtLink to="/">
      Home page
    </NuxtLink>
  </div>
</template>

<script>
export default {
  layout: 'withNavbar',
  asyncData ({ req }) {
    return {
      name: req ? 'server' : 'client'
    }
  }
}
</script>