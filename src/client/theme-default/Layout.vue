<template>
  <div class="theme">
    <header>
      <NavBar />
      <ToggleSideBarButton @toggle="toggleSidebar" />
    </header>
    <aside :class="{ open }">
      <SideBar>
        <template #top>
          <slot name="sidebar-top" />
        </template>
        <template #bottom>
          <slot name="sidebar-bottom" />
        </template>
      </SideBar>
    </aside>
    <div
      class="sidebar-mask"
      :class="{ 'sidebar-open': open }"
      @click="toggleSidebar(false)"
    />
    <main>
      <Page>
        <template #top>
          <slot name="page-top" />
        </template>
        <template #bottom>
          <slot name="page-bottom" />
        </template>
      </Page>
    </main>
  </div>
  <Debug />
</template>

<script>
import { ref } from 'vue'
import NavBar from './components/NavBar.vue'
import ToggleSideBarButton from './components/ToggleSideBarButton.vue'
import SideBar from './components/SideBar.vue'
import Page from './components/Page.vue'

export default {
  components: {
    NavBar,
    ToggleSideBarButton,
    SideBar,
    Page
  },

  setup() {
    const open = ref(false)

    const toggleSidebar = (to) => {
      open.value = typeof to === 'boolean' ? to : !open.value
    }

    return { open, toggleSidebar }
  }
}
</script>
