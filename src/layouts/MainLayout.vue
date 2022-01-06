<template>
  <q-layout view="lHh Lpr lFf">
    <q-header v-if="!isHomePage" elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          3MAuto
        </q-toolbar-title>

        <div>online
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar.png">
          </q-avatar>
        </div>
        
      </q-toolbar>
    </q-header>

   

     <q-drawer v-if="!isHomePage"
        v-model="leftDrawerOpen"
        show-if-above
        :width="200"
        :breakpoint="500"
        bordered
        class="bg-grey-3"
      >
        <q-scroll-area class="fit">
          <q-list padding>
            <q-item 
              v-for="menu in essentialLinks"
              :key="menu.link"
              :to="menu.link"
              clickable
              v-ripple
              exact>
              <q-item-section avatar>
                <q-icon :name="menu.icon" />
              </q-item-section>

              <q-item-section>
                {{menu.title}}
              </q-item-section>
            </q-item>

            
            <q-separator />

            <q-item clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="settings" />
              </q-item-section>

              <q-item-section>
                Settings
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>
      </q-drawer>
    
    <q-page-container>
      <router-view />

      <q-page-sticky v-if="!isHomePage" position="bottom-right" :offset="[18, 18]">
        <q-btn fab icon="add" color="primary" />
      </q-page-sticky>

    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

const linksList = [
  {
    title: 'Home',
    icon: 'home',
    link: '/home'
  },
  {
    title: 'Products',
    icon: 'drafts',
    link: '/productos'
  },
 
  {
    title: 'Sair',
    icon: 'send',
    link: '/'
  },
   
  /* {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  }, */
/*   {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  }, */
/*   {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  }, */
 /*  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev'
  }, */
 /*  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev'
  }, */
  /* {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev'
  } */
];

import { defineComponent, ref } from 'vue'

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
  },

  computed:{
    isHomePage (){
      let route = this.$route.fullPath
      return route==='/'
    }
  }
})
</script>
