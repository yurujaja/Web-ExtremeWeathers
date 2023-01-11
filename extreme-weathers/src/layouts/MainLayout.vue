<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated class="text-white">
      <q-toolbar>
        <!--        <q-btn dense flat round icon="menu" @click="left = !left" />-->

        <q-toolbar-title>
          <q-icon class="text-dark q-ma-md-lg" size="70px">
            <img
              src="icons/project-icon.png"
              style="width: 50px; height: 50px"
            />
          </q-icon>

          Extreme Weather & Climate Change
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <!-- Main content -->
    <q-page-container style="height: 100vh; text-align: center; padding-top: 0">
      <IndexPage />

      <!-- place QPageScroller at end of page -->
      <q-page-scroller
        position="bottom-right"
        :scroll-offset="150"
        :offset="[18, 18]"
      >
        <!-- <q-btn
          fab
          icon="keyboard_arrow_up"
          background="rgba(0, 0, 72, 0.5)"
          style="z-index: 100"
        /> -->
      </q-page-scroller>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import IndexPage from "pages/IndexPage";

export default defineComponent({
  name: "MainLayout",

  components: {
    IndexPage,
  },

  data() {
    return {
      left: false,
    };
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      // essentialLinks: linksList,
      // leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>

<style></style>
