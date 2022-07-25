<template>
      <v-app>
           <v-main>
              <v-container>
                   <v-card>
                       <v-card-title>
                          <h1>Vuetify Form</h1>
                       </v-card-title>
                       <v-card-text> 
                           <v-form ref="form">
                            <v-text-field v-model="title" label="Title" prepend-icon="folder" :rules="inputRules"></v-text-field>
                            <v-textarea v-model="description" label="Write some text here...." :rules="inputRules" prepend-icon="edit" ></v-textarea>
                            
                            <v-menu>
                  <!-- :value="formattedDate"   -->  <v-text-field  slot="activator" label="Due date" :rules="inputRules"></v-text-field>
                                <v-date-picker v-model="due"></v-date-picker>
                            </v-menu>

                            <v-spacer></v-spacer>

                            <v-btn flat class="success" @click="submit" >Add Project</v-btn>
                            </v-form>
                       </v-card-text>
                   </v-card>
              </v-container>
           </v-main>
      </v-app>
</template>

<script>
export default {
    name:'VForm',
    data(){
        return{
            title:'',
            description:'',
            due:null,
            inputRules:[
                v => v.length >= 3 || 'Minimum lenght should be 3 Characters'
            ],
        }
    },
     methods:{
        submit(){
            if(this.$refs.form.validate()){
            console.log(this.title,this.description)
            }
        }
     },
    //  formattedDate(){
    //     return this.due ? formate(this.due, 'Do MMM  YYYY') : ''
    //  }

}
</script>

<style>

</style>