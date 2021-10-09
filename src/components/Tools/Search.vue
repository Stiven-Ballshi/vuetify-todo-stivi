<template>
  <v-text-field
    :value="$store.state.search"
    @input="$store.commit('setSearch', $event)"
    @blur="searchClosed = true"
    @focus="searchClosed = false"
    class="expanding-search mt-2"
    :class="{ 'closed' : searchClosed && !$store.state.search}"
    placeholder="Search"
    :disabled="$store.state.sorting"
    filled
    dense
    clearable
    prepend-inner-icon="mdi-magnify"
  ></v-text-field>
</template>

<script>
export default {
  data() {
    return {
      searchClosed: true
    }
  },
}
</script>

<style lang="scss">
  .expanding-search {
    cursor: pointer!important;
    transition: max-width 0.3s ;
    .v-input__slot {
      cursor: pointer!important;
      &:before , &:after {
        border-color: transparent!important;
      }
    }
    &.closed {
      max-width: 3rem;
      .v-input__slot {
        background: unset !important;
      }
    }
  }
</style>