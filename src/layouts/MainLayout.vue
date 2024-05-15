<template>
  <q-layout view="hHh lpR fFf" class="bg-grey-1">
    <q-header elevated class="bg-white text-grey-8" height-hint="64">
      <q-toolbar class="GNL__toolbar">
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          aria-label="Menu"
          icon="menu"
          class="q-mr-sm"
        />

        <q-toolbar-title
          v-if="$q.screen.gt.xs"
          shrink
          class="row items-center no-wrap"
        >
          <!--   <img
            width="50"
            height="50"
            src="https://img.icons8.com/stickers/100/engineering.png"
            alt="engineering"
          /> -->
          <span class="q-ml-xs" style="font-size: 15px"
            >Barangay Information System Web Base</span
          >
        </q-toolbar-title>

        <q-space />

        <!--  <div class="q-gutter-sm row items-center no-wrap">
          <q-btn round flat>
            <q-avatar size="26px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
            </q-avatar>
            <q-tooltip>Account</q-tooltip>
          </q-btn>
        </div> -->
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-white"
      :width="280"
    >
      <q-scroll-area class="fit">
        <q-list padding class="text-grey-8">
          <q-item class="q-pa-lg">
            <!--   <q-item-section avatar>
              <q-avatar
                rounded
                :class="{
                  'avatar-with-overlay': selectedSection === 'dashboard',
                  'avatar-default': selectedSection !== 'dashboard',
                }"
                text-color="white"
                icon="dashboard"
              >
              </q-avatar>
            </q-item-section> -->

            <q-item-section class="responsive-text">
              <q-item-label> <b>DASHBOARD VIEW</b> </q-item-label>
            </q-item-section>
          </q-item>

          <q-item
            clickable
            @click="handleItemClick"
            :class="{ 'active-item': selectedSection === 'dashboard' }"
          >
            <q-item-section avatar>
              <q-icon
                class="iconcolor"
                size="2.3rem"
                name="dashboard_customize"
              />
            </q-item-section>

            <q-item-section class="responsive-text">
              <q-item-label> <b>Home</b> </q-item-label>
            </q-item-section>
          </q-item>

          <q-expansion-item v-model="management">
            <template v-slot:header>
              <q-item-section avatar>
                <q-icon size="2.3rem" name="today" />
              </q-item-section>
              <q-item-section
                class="responsive-text"
                style="margin-left: -15px"
              >
                <q-item-label style="font-size: 15px">
                  <b>Resident Information</b>
                </q-item-label>
              </q-item-section>
            </template>

            <q-item
              clickable
              @click="toggleSection('health_card')"
              :class="{ 'active-item': selectedSection === 'health_card' }"
            >
              <q-item-section class="q-ml-sm" style="margin-left: -15px">
                <q-item-label>
                  <q-icon
                    size="1.5rem"
                    name="description"
                    class="iconcolor q-ml-md q-mr-md"
                  />
                  Resident Form</q-item-label
                >
              </q-item-section>
            </q-item>

            <!--  <q-item
              clickable
              @click="toggleSection('ToDoos_Two')"
              :class="{ 'active-item': selectedSection === 'ToDoos_Two' }"
            >
              <q-item-section class="q-ml-sm">
                <q-item-label>
                  <q-icon
                    size="1.5rem"
                    name="groups"
                    class="iconcolor q-ml-md q-mr-md"
                  />
                  To Do's 2</q-item-label
                >
              </q-item-section>
            </q-item> -->
          </q-expansion-item>

          <q-expansion-item v-model="settings">
            <template v-slot:header>
              <q-item-section avatar>
                <q-icon size="2.3rem" name="menu_book" />
              </q-item-section>
              <q-item-section class="responsive-text">
                <q-item-label> <b>Blotter Records</b> </q-item-label>
              </q-item-section>
            </template>
            <q-item
              clickable
              v-ripple
              @click="toggleSection('user')"
              :class="{ 'active-item': selectedSection === 'user' }"
            >
              <q-item-section class="q-ml-sm" style="margin-left: -15px">
                <q-item-label>
                  <q-icon
                    size="1.5rem"
                    name="edit_square"
                    class="iconcolor q-ml-md q-mr-md"
                  />
                  Blotter Form</q-item-label
                >
              </q-item-section>
            </q-item>
          </q-expansion-item>

          <q-expansion-item v-model="brgyofficials">
            <template v-slot:header>
              <q-item-section avatar>
                <q-icon size="2.3rem" name="supervisor_account" />
              </q-item-section>
              <q-item-section class="responsive-text">
                <q-item-label> <b>Barangay Officials</b> </q-item-label>
              </q-item-section>
            </template>
            <q-item
              clickable
              v-ripple
              @click="toggleSection('user')"
              :class="{ 'active-item': selectedSection === 'user' }"
            >
              <q-item-section class="q-ml-sm" style="margin-left: -15px">
                <q-item-label>
                  <q-icon
                    size="1.5rem"
                    name="sticky_note_2"
                    class="iconcolor q-ml-md q-mr-md"
                  />
                  Brgy Official Records</q-item-label
                >
              </q-item-section>
            </q-item>
          </q-expansion-item>

          <q-expansion-item v-model="useraccount">
            <template v-slot:header>
              <q-item-section avatar>
                <q-icon size="2.3rem" name="manage_accounts" />
              </q-item-section>
              <q-item-section class="responsive-text">
                <q-item-label> <b>User Account</b> </q-item-label>
              </q-item-section>
            </template>
            <q-item
              clickable
              v-ripple
              @click="toggleSection('user')"
              :class="{ 'active-item': selectedSection === 'useraccount' }"
            >
              <q-item-section class="q-ml-sm" style="margin-left: -15px">
                <q-item-label>
                  <q-icon
                    size="1.5rem"
                    name="sticky_note_2"
                    class="iconcolor q-ml-md q-mr-md"
                  />
                  User
                </q-item-label>
              </q-item-section>
            </q-item>
          </q-expansion-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>
    <!-- <q-page-container>
      <router-view />
    </q-page-container> -->
    <q-page-container v-if="DashboardView">
      <DashboardView />
    </q-page-container>
    <q-page-container v-if="showHealthCard">
      <Health_card />
    </q-page-container>
    <q-page-container v-if="showTodosTwo">
      <ToDoos_Two />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
// import EssentialLink from "components/EssentialLink.vue";
import Health_card from "components/Health_card.vue";
import ToDoos_Two from "components/ToDoos_Two.vue";
import DashboardView from "src/components/DashboardView.vue";

const linksList = [
  {
    title: "Admin",
    // caption: 'quasar.dev',
    caption: "",
    icon: "home",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    // EssentialLink,
    Health_card,
    ToDoos_Two,
    DashboardView,
  },

  setup() {
    const leftDrawerOpen = ref(true);
    const settings = ref(true);
    const management = ref(true);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      settings,
      management,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },

  data() {
    return {
      selectedSection: "dashboard",
      DashboardView: true,
      showHealthCard: false,
      showTodosTwo: false,
      brgyofficials: true,
      useraccount: true,
    };
  },
  methods: {
    handleItemClick() {
      // Call both functions here
      this.toggleSection("dashboard");
    },

    /*   toggleSubMenu() {
      this.submenuOpen = !this.submenuOpen;
    }, */

    /*   closeSubMenu() {
      this.submenuOpen = false;
    }, */
    toggleSection(section) {
      this.showHealthCard = section === "health_card";
      this.showTodosTwo = section === "ToDoos_Two";
      this.DashboardView = section === "dashboard";
      if (section === "dashboard") {
        this.management = true; // Close management expansion item
        this.settings = true; // Close settings expansion item
      } else {
      }
      if (this.selectedSection === section) {
        // If the clicked section is already open, close it
        this.selectedSection = null;
      } else {
        this.selectedSection = null;
        this.selectedSection = section;
      }
    },
  },
});
</script>
<style scoped>
.iconcolor {
  color: rgba(12, 156, 10, 0.701);
}

.avatar-default {
  background: linear-gradient(
    40deg,
    #279f27,
    #5fc331
  ); /* Gradient from green to white */
}

.avatar-with-overlay {
  position: relative; /* Set position to relative */
}

.avatar-with-overlay::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    40deg,
    #279f27,
    #5fc331
  ); /* Gradient from green to white */

  border-radius: inherit; /* Inherit border radius from the avatar */
}

.GNL__toolbar {
  height: 64px;
}

.GNL__toolbar-input {
  width: 55%;
}

.GNL__drawer-item {
  line-height: 24px;
  border-radius: 0 24px 24px 0;
  margin-right: 12px;
}

.GNL__drawer-item .q-item__section--avatar .q-icon {
  color: #5f6368;
}

.GNL__drawer-item .q-item__label {
  color: #3c4043;
  letter-spacing: 0.01785714em;
  font-size: 0.875rem;
  font-weight: 500;
  line-height: 1.25rem;
}

.GNL__drawer-footer-link {
  color: inherit;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.75rem;
}

.GNL__drawer-footer-link:hover {
  color: #000;
}
</style>
