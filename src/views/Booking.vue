<template>
  <v-container style="margin-top: 50px; margin-left: 80px;">
    <v-row d-flex>
      <div class="input-container">
        <v-row class="input-content mt-5">
            <v-form v-model="test">
            <v-row>
              <v-col>
                <p class="mb-0">First Name*</p>
                <v-text-field class="mediumInput" hide-details v-model="firstName"
                ></v-text-field>
              </v-col>
              <v-col>
                <p>Last Name*</p>
                <v-text-field class="mediumInput"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>
                <p>Phone*</p>
                <v-text-field class="mediumInput"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>              
                <p>Email*</p>
                <v-text-field class="largeInput"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>              
                <p>Pick a Date</p>
                <v-text-field class="mediumInput"></v-text-field>
              </v-col>
              <v-col>              
                <p>Pick a Time</p>
                <v-text-field class="mediumInput"></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col>            
                <p>Choose a Service</p>
                <v-text-field class="largeInput"></v-text-field>
              </v-col>
            </v-row>
            <v-row class="requestButton">
              <v-btn>Request an Appointment</v-btn>
            </v-row>
          </v-form>
          </v-row>
        </div>
        <div class="bookingDescription">Description of product along with expected pricing.</div>
      </v-row>
    </v-container>
</template>

<script>
export default {
  name: "BookingView",

  data: () => ({
    firstName: "",
  }),
};
</script>

<style scoped>
.input-container {
  width: 710px;
  height: 565px;
  background-color: #DCA7A7;
  box-shadow: -10px 10px 2px 0 rgb(115 91 91);
  color: black;
  font-weight: 500;
}
.input-content {
  margin-left: 30px;
  margin-top: 10px;
}
.v-input.v-text-field {
  background-color: white;
  border-style: solid;
  border-radius: 3px;
}

.v-input.v-text-field>.v-input__control {
  margin-left: 5px;
}
.mediumInput {
  width: 312px;
  height: 50px;
}

.largeInput {
  width: 650px;
  height: 50px;
}
.v-input.v-text-field>.v-input__control>.v-input__slot:before {
    border: none;
}
.v-input.v-text-field>.v-input__control>.v-input__slot:after {
    border: none;
}

.v-input.v-text-field>.v-input__control>.v-text-field__slot {
  max-height: 20px;
}
.bookingDescription {
  color: black;
  font-weight: 500;
  margin-left: 20px;
  width: 200px;
}
.requestButton {
  display: flex;
  justify-content: center;
  .v-btn {
    border: 1px solid black;
  }
}
</style>
