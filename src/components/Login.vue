<template>
  <div id="app">
      <v-app>
        <v-main>
            <v-layout align-center>
                <v-container style="width: 250px" >
                    
                   <v-row justify="center">
                        <v-card width="400" height="250">
                    <v-card-title class="text-center">
                        Fitness App
                    </v-card-title>

                    <v-card-text>
                        <v-row>
                        <v-col class="my-0" cols="12">
                            <v-text-field type="email" label="Email" dense />
                        </v-col>

                        <v-col class="my-0" cols="12">
                            <v-text-field
                                v-model="password"
                                :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                                :rules="[rules.required, rules.min]"
                                :type="show1 ? 'text' : 'password'"
                                name="input-10-1"
                                label="Password"
                                hint="At least 8 characters"
                                counter
                                dense
                                @click:append="show1 = !show1"
                            ></v-text-field>
                        </v-col>
                        </v-row>
                    </v-card-text>
                    <v-card-actions class="float-right">
                        <v-btn
                            depressed
                            color="primary"
                        >
                            Login
                        </v-btn>
                    </v-card-actions>
                    </v-card>
                   </v-row>
                </v-container>
            </v-layout>
        </v-main>
      </v-app>
  </div>

</template>

<script>
export default {
  name: 'App',
  data () {
      return {
        show1: false,
        show2: true,
        email: "",
        password: "",
        rules: {
          required: value => !!value || 'Required.',
          min: v => v.length >= 8 || 'Min 8 characters',
          emailMatch: () => (`The email and password you entered don't match`),
        },
      }
    }
}
</script>

<style>

</style>
