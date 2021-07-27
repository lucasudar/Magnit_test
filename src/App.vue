<template>
  <v-app>
    <v-app-bar app
               color="blue"
               flat>
      <div class="navbar-component">
        <a href="https://magnit.ru/" class="brand">Brand</a>
        <a href="#" class="item-link">Home</a>
      </div>

    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main>

      <!-- Provides the application the proper gutter -->
      <v-container fluid>

        <Rates></Rates>
        <Cards></Cards>
        <Table></Table>

      </v-container>
    </v-main>

    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  components: {
    Rates: () => import('./components/Rates'),
    Cards: () => import('./components/Cards'),
    Table: () => import('./components/Table'),
  },

  data: () => ({
    //
  }),
};
</script>
<style>
.navbar-component {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
}
.item-link {
  margin: 0 0 0 20px ;
}
</style>