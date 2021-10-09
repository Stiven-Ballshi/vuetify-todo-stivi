<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer"
      app
      :mobile-breakpoint="768"
      >
      <v-img
        height="170"
        src="../public/mountains.jpg"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        class="pa-4 pt-7"
      >
        <v-avatar size="65" class="mb-2">
        <img
          src="https://cdn.vuetifyjs.com/images/john.jpg"
          alt="John" 
        >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">Stiven Ballshi</div>
        <div class="white--text text-subtitle-2">stiven_ballshi</div>
      </v-img>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      prominent
      :height="$route.path === '/' ? '238' : '170' "
      src="../public/mountains.jpg"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="header-container pa-3">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
         <v-row>
           <v-toolbar-title class="text-h4">{{ $store.state.appTitle }}</v-toolbar-title>
        </v-row>
        <v-row>
          <live-date-time></live-date-time>
        </v-row>
        <v-row v-if="$route.path === '/' ">
          <field-add-task />
        </v-row>
      </v-container>

    </v-app-bar>

    <v-main>
      <router-view />
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Search from '@/components/Tools/Search.vue'
import LiveDateTime from '@/components/Tools/LiveDateTime.vue'
import FieldAddTask from '@/components/Todo/FieldAddTask.vue'
import Snackbar from '@/components/Shared/Snackbar.vue'

  export default {
    data: () => ({ 
      drawer: null,
      items: [
        { 
          title: 'Todo',
          icon: 'mdi-format-list-checks', 
          to:'/'
        },
        { 
          title: 'About', 
          icon: 'mdi-help-box', 
          to:'/about' 
        }
      ] 
    }),
    mounted() {
      this.$store.dispatch('getTasks')
    },
    components: {
      'snackbar' : Snackbar,
      'live-date-time' : LiveDateTime,
      'field-add-task' : FieldAddTask,
      'search' : Search
    }
  }
</script>

<style lang="scss">
  .header-container {
    max-width: none !important;
  }
</style>