<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

      </q-toolbar>
      <div class="q-px-lg  q-mb-md">
        <div class="text-h3">Todo</div>
      </div>
    </q-header>

    <q-footer>
      <q-tabs>
        <q-route-tab

        to="/"
        icon="list"
        label="Todo" />

        <q-route-tab
        to="/settings"
        icon="settings"
        label="Settings" />

      </q-tabs>
    </q-footer>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="160"
        :breakpoint="600"
      >

          <q-list padding>
            <q-item
              to="/"
              exact
              clickable
              v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                Todo
              </q-item-section>
            </q-item>

            <q-item
              to="/settings"
              exact
              clickable
              v-ripple>
              <q-item-section avatar>
                <q-icon name="settings" />
              </q-item-section>

              <q-item-section>
                Settings
              </q-item-section>
            </q-item>

          </q-list>


      </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {

    title: 'Todo',
    icon: 'list',
    link: '/',

  },
  {
    title: 'Settings',
    icon: 'settings',
    link: '/#/settings'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>
