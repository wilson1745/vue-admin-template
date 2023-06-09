<template>
  <v-list-group :prepend-icon="prependIcon">
    <v-list-tile slot="activator">
      <v-list-tile-title class="item-title">{{
        $t(titleKey)
      }}</v-list-tile-title>
    </v-list-tile>
    <v-list-tile
      v-for="item in items"
      :key="item.title"
      @click="changeRoute(item.route)"
    >
      <v-list-tile-action>
        <v-icon>{{ item.icon }}</v-icon>
      </v-list-tile-action>
      <v-list-tile-title
        :class="[
          { active: selectedIndex === item.route.params.id },
          'item-title',
        ]"
      >
        {{ item.titleKey ? $t(item.titleKey) : item.title }}
      </v-list-tile-title>
    </v-list-tile>
  </v-list-group>
</template>

<script>
export default {
  props: {
    prependIcon: {
      type: String,
      required: true,
    },
    titleKey: {
      type: String,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
    selectedIndex: {
      type: Number,
      default: -1,
    },
  },
  methods: {
    changeRoute(route) {
      this.$router.push(route);
    },
  },
};
</script>

<style>
</style>
