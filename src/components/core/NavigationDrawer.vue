<template>
  <v-navigation-drawer v-model="toggle" fixed app>
    <v-toolbar flat dark :color="$root.themeColor" class="toolbar">
      <router-link :to="{ name: 'Dashboard' }">
        <img src="static/logo.png" width="36px" />
        <!-- <span class="text">Vue Admin Template</span> -->
      </router-link>
      <router-link :to="{ name: 'Dashboard' }" class="text">
        Vue Admin Template
      </router-link>
    </v-toolbar>

    <v-list>
      <v-list-tile
        v-for="item in menuItems"
        :key="item.route"
        @click="changeRoute(item.route, item.selectedIndex)"
      >
        <v-list-tile-action>
          <v-icon>{{ item.icon }}</v-icon>
        </v-list-tile-action>
        <v-list-tile-title
          :class="[
            { active: selectedIndex === item.selectedIndex },
            'item-title',
          ]"
          >{{ $t(item.title) }}</v-list-tile-title
        >
      </v-list-tile>

      <v-list>
        <v-list-group
          v-for="(group, index) in menuGroups"
          :key="index"
          :prepend-icon="group.icon"
        >
          <v-list-tile slot="activator">
            <v-list-tile-title class="item-title">{{
              $t(group.title)
            }}</v-list-tile-title>
          </v-list-tile>
          <v-list-tile
            v-for="(subItem, subIndex) in group.items"
            :key="subIndex"
            @click="changeRoute(subItem.route, subItem.selectedIndex)"
            :class="{ active: selectedIndex === subItem.selectedIndex }"
          >
            <v-list-tile-action>
              <v-icon>{{ subItem.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-title
              :class="[
                { active: selectedIndex === subItem.selectedIndex },
                'item-title',
              ]"
              >{{ $t(subItem.title) }}</v-list-tile-title
            >
          </v-list-tile>
        </v-list-group>
      </v-list>

      <!-- <v-list>
        <CustomListGroup
          prependIcon="pageview"
          titleKey="widgets"
          :items="widgetItems"
        />
        <CustomListGroup
          prependIcon="select_all"
          titleKey="overlays"
          :items="overlayItems"
        />
        <CustomListGroup
          prependIcon="fingerprint"
          titleKey="authorization"
          :items="authorizationItems"
        />
        <CustomListGroup
          prependIcon="account_circle"
          titleKey="users"
          :items="userItems"
        />
      </v-list> -->

      <!-- <v-list-group prepend-icon="pageview">
        <v-list-tile slot="activator">
          <v-list-tile-title class="item-title">{{
            $t("widgets")
          }}</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="changeRoute('Social', 5)">
          <v-list-tile-action>
            <v-icon>group</v-icon>
          </v-list-tile-action>
          <v-list-tile-title
            :class="[{ active: selectedIndex === 5 }, 'item-title']"
            >{{ $t("social") }}</v-list-tile-title
          >
        </v-list-tile>
        <v-list-tile @click="changeRoute('Chart', 6)">
          <v-list-tile-action>
            <v-icon>bar_chart</v-icon>
          </v-list-tile-action>
          <v-list-tile-title
            :class="[{ active: selectedIndex === 6 }, 'item-title']"
            >{{ $t("charts") }}</v-list-tile-title
          >
        </v-list-tile>
        <v-list-tile @click="changeRoute('Media', 7)">
          <v-list-tile-action>
            <v-icon>perm_media</v-icon>
          </v-list-tile-action>
          <v-list-tile-title
            :class="[{ active: selectedIndex === 7 }, 'item-title']"
            >{{ $t("media") }}</v-list-tile-title
          >
        </v-list-tile>
      </v-list-group>

      <v-list-group prepend-icon="select_all">
        <v-list-tile slot="activator">
          <v-list-tile-title class="item-title">{{
            $t("overlays")
          }}</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="changeRoute('Snackbar', 8)">
          <v-list-tile-action>
            <v-icon>event_note</v-icon>
          </v-list-tile-action>
          <v-list-tile-title
            :class="[{ active: selectedIndex === 8 }, 'item-title']"
            >{{ $t("snackbar") }}</v-list-tile-title
          >
        </v-list-tile>
      </v-list-group>

      <v-list-group prepend-icon="fingerprint">
        <v-list-tile slot="activator">
          <v-list-tile-title class="item-title">{{
            $t("authorization")
          }}</v-list-tile-title>
        </v-list-tile>

        <v-list-tile
          @click="$router.push({ name: 'Error', params: { errorCode: '403' } })"
        >
          <v-list-tile-action>
            <v-icon>cancel</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="item-title">403</v-list-tile-title>
        </v-list-tile>

        <v-list-tile
          @click="$router.push({ name: 'Error', params: { errorCode: '404' } })"
        >
          <v-list-tile-action>
            <v-icon>cancel</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="item-title">404</v-list-tile-title>
        </v-list-tile>

        <v-list-tile
          @click="$router.push({ name: 'Error', params: { errorCode: '500' } })"
        >
          <v-list-tile-action>
            <v-icon>cancel</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="item-title">500</v-list-tile-title>
        </v-list-tile>

        <v-list-tile @click="$router.push({ name: 'Login' })">
          <v-list-tile-action>
            <v-icon>cancel</v-icon>
          </v-list-tile-action>
          <v-list-tile-title class="item-title">{{
            $t("login")
          }}</v-list-tile-title>
        </v-list-tile>
      </v-list-group>

      <v-list-group prepend-icon="account_circle">
        <v-list-tile slot="activator">
          <v-list-tile-title class="item-title">{{
            $t("users")
          }}</v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon v-text="'people_outline'"></v-icon>
          </v-list-tile-action>
          <v-list-tile-title v-text="'Management'"></v-list-tile-title>
        </v-list-tile>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon v-text="'settings'"></v-icon>
          </v-list-tile-action>
          <v-list-tile-title v-text="'Settings'"></v-list-tile-title>
        </v-list-tile>
      </v-list-group> -->
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  props: {
    toggle: {
      type: Boolean,
      required: false,
      default: true,
    },
  },

  data() {
    return {
      selectedIndex: 1,
      menuItems: [
        {
          title: "Getting Start",
          route: "GettingStart",
          icon: "bar_chart",
          selectedIndex: 1,
        },
        {
          title: "Dashboard",
          route: "Dashboard",
          icon: "dashboard",
          selectedIndex: 2,
        },
        {
          title: "Calendar",
          route: "Calendar",
          icon: "calendar_today",
          selectedIndex: 3,
        },
        { title: "Mailbox", route: "Mailbox", icon: "mail", selectedIndex: 4 },
        {
          title: "Studying Vue",
          route: "studyingvue",
          icon: "perm_media",
          selectedIndex: 9,
        },
      ],
    };
  },

  computed: {
    menuGroups() {
      return [
        {
          title: "Widgets",
          icon: "pageview",
          items: [
            {
              title: "Social",
              route: "Social",
              icon: "group",
              selectedIndex: 5,
            },
            {
              title: "Chart",
              route: "Chart",
              icon: "bar_chart",
              selectedIndex: 6,
            },
            {
              title: "Media",
              route: "Media",
              icon: "perm_media",
              selectedIndex: 7,
            },
          ],
        },
        {
          title: "Overlays",
          icon: "select_all",
          items: [
            {
              title: "Snackbar",
              route: "Snackbar",
              icon: "event_note",
              selectedIndex: 8,
            },
          ],
        },
        {
          title: "Authorization",
          icon: "fingerprint",
          items: [
            {
              title: "403",
              route: "Error",
              icon: "cancel",
              params: { errorCode: "403" },
            },
            {
              title: "404",
              route: "Error",
              icon: "cancel",
              params: { errorCode: "404" },
            },
            {
              title: "500",
              route: "Error",
              icon: "cancel",
              params: { errorCode: "500" },
            },
            { title: "Login", route: "Login", icon: "cancel" },
          ],
        },
        {
          title: "Users",
          icon: "account_circle",
          items: [
            { title: "Management", icon: "people_outline", selectedIndex: 50 },
            { title: "Settings", icon: "settings", selectedIndex: 51 },
          ],
        },
      ];
    },
  },

  methods: {
    changeRoute(routeName, selectedIndex) {
      const vm = this;
      vm.selectedIndex = selectedIndex;
      return vm.$router.push({ name: routeName });
    },
  },
};
</script>

<style>
.toolbar {
  font-weight: bold;
  font-size: 18px;
}

.toolbar .text {
  padding-left: 15px;
  color: white;
  text-decoration: none;
}

.item-title {
  font-size: 17px;
  font-weight: 500;
}
.item-sub-title {
  font-size: 15px;
  font-weight: 500;
}

.active {
  font-weight: bold;
}
</style>
