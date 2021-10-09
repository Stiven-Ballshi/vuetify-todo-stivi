<template>
  <div>
    <v-list-item
      @click="$store.dispatch('doneTask', task.id)"
      :class="{ 'blue lighten-5' : task.done }"
      :ripple="false"
      class="white"
      >
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox
            :input-value="task.done"
            color="primary"
          ></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title :class="{'text-decoration-line-through' : task.done }">{{ task.title }}</v-list-item-title>
        </v-list-item-content>

        <v-list-item-action v-if="task.dueDate">
          <v-list-item-action-text>
            <v-icon>mdi-calendar</v-icon>
            {{ task.dueDate | niceDate}}
          </v-list-item-action-text>
        </v-list-item-action>

        <v-list-item-action>
        <task-menu :task="task"/>
      </v-list-item-action>

       <v-list-item-action v-if="$store.state.sorting">
         <v-btn
          color="primary"
          icon
          class="handle"
        >
          <v-icon>mdi-drag-horizontal-variant</v-icon>
        </v-btn>
      </v-list-item-action>

      </template> 
    </v-list-item>
    <v-divider></v-divider>
    
  </div>
</template>

<script>
import { format } from 'date-fns'
import TaskMenu from '@/components/Todo/TaskMenu.vue'

export default {
  props: ['task'],
  components: {
    'task-menu' : TaskMenu
  },
  filters: {
    niceDate(value) {
      return format(new Date(value), 'MMM d')
    }
  }
}
</script>

<style lang="scss">
  .sortable-ghost {
    opacity: 0;
  }
  .sortable-drag {
    box-shadow: 0 0 10px rgba(0,0,0,0.3)
  }
</style>