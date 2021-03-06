<template>
  <div class="birdseye-app">
    <div class="app-inner">
      <aside class="app-side">
        <NavSide
          :nav="nav"
          :meta="$route.params.meta"
          :pattern="$route.params.pattern"
        />
      </aside>

      <main
        ref="slot"
        class="app-preview"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { ComponentMeta } from '@birdseye/core'
import NavSide from './components/NavSide.vue'

export default Vue.extend({
  components: {
    NavSide
  },

  props: {
    nav: {
      type: Array as () => ComponentMeta[],
      default: () => []
    }
  },

  mounted() {
    // Hack for avoid processing slot in Vue
    const slot = document.createElement('slot')
    const wrapper = this.$refs.slot as HTMLElement
    wrapper.appendChild(slot)
  }
})
</script>

<style src="k-css/k.css">
</style>

<style>
:host {
  --color-base: #f1f8fd;
  --color-main: #828bec;
  --color-preview-background: #fff;
  --width-side: 280px;
  --padding-preview: 20px;
  --ease-out-cubic: cubic-bezier(0.215, 0.61, 0.355, 1);
  --font-family-base: -apple-system, BlinkMacSystemFont, 'Helvetica Neue',
    'Segoe UI', sans-serif;
}
</style>

<style scoped>
.birdseye-app {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}

.app-inner {
  display: flex;
  width: 100%;
  height: 100%;
}

.app-side {
  all: initial;
  font-family: var(--font-family-base);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  overflow: auto;
  flex: none;
  padding: 20px;
  width: var(--width-side);
  background-color: var(--color-base);
}

.app-preview {
  overflow: auto;
  flex: 1 1 auto;
  padding: var(--padding-preview);
  background-color: var(--color-preview-background);
}
</style>
