<template>
  <!-- Normal General Table with Get Request -->
     <v-app> 
        <v-main> 
             <v-container>
        <h1>Normal Table Vue  Vuetify</h1>
             <table class="table table-bordered table table-dark table-striped">
                  <thead>
                      <tr>
                          <th>Id</th>
                          <th>E-Mail</th>
                          <th>Firstname</th>
                          <th>Lastname</th>
                          <th>Profile Pic</th>
                      </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(data,index) in tableData" :key="index" >
                        <td v-text="data.id"></td>
                        <td v-text="data.email"></td>
                        <td v-text="data.first_name"></td>
                        <td v-text="data.last_name"></td>
                        <td> <img :src="data.avatar" alt="" width="40" class="rounded-circle"> </td>
                    </tr>
                  </tbody>
             </table>
    <!-- Simple Table with Vuetify -->
    <h1>Simple Vue Table Vuetify</h1>
    <v-simple-table dark>
        <template v-slot:default>
                 <thead>
                      <tr>
                          <th class="text left">Id</th>
                          <th class="text left">E-Mail</th>
                          <th class="text left">Firstname</th>
                          <th class="text left">Lastname</th>
                          <th class="text left">Profile Pic</th>
                      </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(data,index) in tableData" :key="index" >
                        <td v-text="data.id"></td>
                        <td v-text="data.email"></td>
                        <td v-text="data.first_name"></td>
                        <td v-text="data.last_name"></td>
                        <td> <img :src="data.avatar" alt="" width="40" class="rounded-circle"> </td>
                    </tr>
                  </tbody>        
        </template>
    </v-simple-table>

     <!-- Advanced Table with Vuetify -->
     <h1 class="mt-5">Advanced Table with Vuetify</h1>

     <template >
        <v-row>
            <v-col md="3">
                <v-text-field v-model="search" append-icon="mdi-magnify" label="Search..." single-line hide-details></v-text-field>
            </v-col>
        </v-row>

        <v-row>
            <v-col>
                 <v-data-table dark :headers="headers" :items="vtable" :items-per-page="7" :search="search" class="elevation-1">
                    <template v-slot:item.="{item}" >
                              <v-icon small @click="deleteUser(item.id)" > mdi-delete </v-icon>
                    </template>
                 </v-data-table>
            </v-col>
        </v-row>
        
     </template>
    <template></template>
         </v-container>
      </v-main> 
    </v-app>
</template>

<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios, axios);

export default {
    name:'Tables',
    data(){
        return{
            tableData:[],
            search:'',
            headers:[{text:"Id",value:'id',align:'start',sortable:false},
                     {text:"Email",value:"email"},
                     {text:"FirstName",value:"first_name"},
                     {text:"LastName",value:"last_name"},
                     {text:"Actions",value:"actions", sortable:false},
                     ],
            vtable:[{id:7,email:"michael.lawson@reqres.in",first_name:"Michael",last_name:"Lawson",avatar:"https://reqres.in/img/faces/7-image.jpg"},
                    {id:8,email:"lindsay.ferguson@reqres.in",first_name:"Lindsay",last_name:"Ferguson",avatar:"https://reqres.in/img/faces/8-image.jpg"},
                    {id:9,email:"tobias.funke@reqres.in",first_name:"Tobias",last_name:"Funke",avatar:"https://reqres.in/img/faces/9-image.jpg"},
                    {id:10,email:"byron.fields@reqres.in",first_name:"Byron",last_name:"Fields",avatar:"https://reqres.in/img/faces/10-image.jpg"},
                    {id:11,email:"george.edwards@reqres.in",first_name:"George",last_name:"Edwards",avatar:"https://reqres.in/img/faces/11-image.jpg"},
                    {id:12,email:"rachel.howell@reqres.in",first_name:"Rachel",last_name:"Howell",avatar:"https://reqres.in/img/faces/12-image.jpg"}]
        }
    },
    methods:{
           getUserData(){
                axios.get('https://reqres.in/api/users?page=2').then( res =>{
                this.tableData = res.data.data
                console.log(res.data.data)
                      }).catch((error)=>{
                console.log("Error in Get Api Call",error);
            })
           },
           deleteUser(id){
               const index=this.vtable.indexOf((x)=> x.id===id )
               this.vtable.splice(index,1);
           }
    },
    mounted(){
            this.getUserData();   //We can write the axios get code here also- wont get any error- We are just using the method here   
            // Vue.axios.get('https://reqres.in/api/users?page=2').then( res =>{
            //     this.tableData = res.data.data
            //     console.log(res.data.data)
            //           }).catch((error)=>{
            //     console.log("Error in Get Api Call",error);
            // }) 
         
    }

}
</script>

<style scoped>
   /* table, th, td {
  border: 1px solid black;
  border-collapse: collapse; */

</style>
