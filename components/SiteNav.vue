<template>
  <nav
    class="navbar has-shadow is-fixed-top"
    role="navigation"
    aria-label="main navigation"
  >
    <div class="container">
      <div class="navbar-brand">
        <nuxt-link class="navbar-item" to="/">
          <site-logo v-if="$siteConfig.logo === 'logo-component'" />
          <img
            v-else
            style="height: 100px; width auto;"
            :src="$siteConfig.logo"
            :alt="$siteConfig.siteName"
            class="logo"
          />&nbsp;The Ben Dungan (dot com)
        </nuxt-link>
        <hamburger-button @click="active = !active" />
      </div>

      <div
        :class="{
          'navbar-menu': true,
          'is-active': active
        }"
      >
        <ul class="navbar-end">
          <li
            v-for="item in $siteConfig.mainMenu"
            :key="item.link"
            class="navbar-item"
            @click="active = false"
          >
            <component
              :is="item.link.startsWith('http') ? 'a' : 'nuxt-link'"
              :href="item.link"
              :to="item.link"
              :target="item.target ? item.target : '_self'"
            >
              {{ item.name }}
            </component>
          </li>
          <div class="navbar-item has-dropdown is-hoverable">
            <li class="navbar-item has-text-black-ter">
              <a class="has-text-black-ter navbar-link">
                Social Media
              </a>
            </li>

            <div class="navbar-dropdown">
              <a
                class="navbar-item"
                href="https://www.instagram.com/bldungan/"
                target="_blank"
              >
                Instagram
              </a>
              <a
                class="navbar-item"
                href="https://twitter.com/thebendungan"
                target="_blank"
              >
                Twitter
              </a>
              <a
                class="navbar-item"
                href="https://www.linkedin.com/in/ben-dungan-7008507/"
                target="_blank"
              >
                Linkedin
              </a>
            </div>
          </div>
          <li class="navbar-item has-text-black-ter site-search-wrapper">
            <site-search />
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
import SiteSearch from '~/components/SiteSearch'
import HamburgerButton from '~/components/HamburgerButton'
export default {
  name: 'SiteNav',
  components: { SiteSearch, HamburgerButton },
  data() {
    return {
      active: false
    }
  }
}
</script>
<style lang="scss" scoped>
.site-search-wrapper {
  transform: translateX(5px);
  @media (max-width: 1023px) {
    display: none;
  }
}
.navbar-burger {
  height: auto;
}

.navbar-menu a {
  display: block;
}
</style>
