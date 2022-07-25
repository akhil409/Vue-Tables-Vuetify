<template>
  <!-- <v-app>
      <v-content><Tables /></v-content>
   <v-main>
      <Tables />
    </v-main>
  </v-app> -->
      <div>
         <Tables />
         <!-- <VForm /> -->
     </div>
</template>

<script>
import Tables from './components/Tables.vue';
// import VForm from './components/VForm.vue';


export default {
  name: 'App',

  components: {
    Tables,
    // VForm,
},

  data: () => ({
    //
  }),
};
</script>
