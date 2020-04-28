<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <NuxtLink class="navbar-item" to="/">
          Easy Github Labels
        </NuxtLink>

        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>

    <section class="main-content columns">
      <div class="container column is-12">
        <nuxt />
      </div>
    </section>
    <footer>
      <p class="has-text-grey">
        <a href="https://github.com/ddarkr/easy-github-labels">Github</a> /
        Using
        <a href="https://github.com/jvandemo/copy-github-labels"
          >copy-github-labels</a
        >
        / Built with Nuxt.js and Buefy
      </p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  }
}
</script>

<style scoped>
footer {
  text-align: center;
  margin-top: 32px;
}
</style>
