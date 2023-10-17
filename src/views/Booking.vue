<template>
  <v-container style="margin-top: 50px; margin-left: 80px;">
    <v-row d-flex>
      <div class="input-container">
        <v-row class="input-content mt-5">
            <v-form id="bookingForm">
            <v-row>
              <v-col>
                <p class="mb-0">First Name*</p>
                <v-text-field class="mediumInput" hide-details name="firstName" v-model="firstName" placeholder="John"
                ></v-text-field>
              </v-col>
              <v-col>
                <p>Last Name*</p>
                <v-text-field class="mediumInput" name="lastName" v-model="lastName" placeholder="Doe"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>
                <p>Phone*</p>
                <v-text-field class="mediumInput" name="phoneNumber" v-model="phoneNumber" placeholder="(###) ###-####"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>              
                <p>Email*</p>
                <v-text-field class="largeInput" name="email" v-model="email" placeholder="john.doe@email.com"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>
                <p>Street Address</p>
                <v-text-field class="mediumInput" name="streetName" v-model="streetName" placeholder="1234 Street Name"></v-text-field>
              </v-col>
              <v-col>
                <p>City</p>
                <v-text-field class="mediumInput" name="cityName" v-model="cityName" placeholder="City"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>
                <p>State</p>
                <v-text-field class="mediumInput" name="stateName" v-model="stateName" placeholder="State"></v-text-field>
              </v-col>
              <v-col>
                <p>ZIP Code</p>
                <v-text-field class="mediumInput" name="zipCode" v-model="zipCode" placeholder="12345"></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col>              
                <p>Date</p>
                <!--v-text-field class="mediumInput"></v-text-field!-->
                <date-picker 
                  class="mediumInput datePicker"
                  type="date"
                  name="date" 
                  v-model="dateRequest" 
                  valueType="format" 
                  format="MM-DD-YYYY"
                  placeholder="MM-DD-YYYY"
                  partial-update="true"
                  @focusout.native="$refs.datepicker.closePopup" 
                  ></date-picker>
              </v-col>
              <v-col>              
                <p>Time</p>
                <date-picker 
                  class="mediumInput datePicker"
                  type="time" 
                  name="time"
                  v-model="time"
                  valueType="format"
                  format="h:mm A"
                  placeholder="Select a Time"
                  minute-step="30"  
                  show-second="false"
                  :time-picker-options="timeOptions"
                  @focusout.native="$refs.datepicker.closePopup" 
                ></date-picker>
              </v-col>
            </v-row>
            <v-row>
              <v-col>            
                <p>Notes</p>
                <v-text-field class="largeInput" name="message" v-model="message" placeholder="Special request or notes here.."></v-text-field>
              </v-col>
            </v-row>
            <v-row class="requestButton">
              <v-btn @click="sendEmail()">Request an Appointment</v-btn>
            </v-row>
          </v-form>
          </v-row>
        </div>
        <div class="bookingDescription">Description of product along with expected pricing.</div>
      </v-row>
    </v-container>
</template>

<script>
import emailjs from 'emailjs-com';
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';

export default {
  name: "BookingView",
  components: {
    DatePicker,
  },

  data: () => ({
    firstName: "",
    lastName: "",
    phoneNumber: "",
    email: "",
    streetName: "",
    cityName: "",
    stateName: "",
    zipCode: "",
    dateRequest: "",
    time: "",
    message: "",

    timeOptions: { start: '7:00', step: '00:30', end: '22:00', format: 'h:mm A'},
  }),
  methods: {
    sendEmail() {
      /*if (this.firstName == "") {
        alert("First Name field is empty");
        document.getElementById("contactFirstName").focus();
      } else if (this.lastName == "") {
        alert("Last Name field is empty");
        document.getElementById("contactLastName").focus();
      } else if (this.phoneNumber == "" || this.phoneNumber.length < 9) {
        alert("Please enter a valid phone number.");
        document.getElementById("contactPhoneNumber").focus();
      } else if (this.email == "") {
        alert("Please enter a valid email address.");
        document.getElementById("contactEmailAddress").focus();
      }  else if (this.message == "") {
        alert("Please enter a valid message.");
        document.getElementById("contactMessage").focus();
      } else {*/
      try {
        emailjs.sendForm('service_2grbipg', 'template_patfz0a', "#bookingForm" ,"bJYwKkriG105jLWq8", {
          firstName: this.firstName,
          lastName: this.lastName,
          phoneNumber: this.phoneNumber,
          email: this.email,
          streetName: this.streetName,
          cityName: this.cityName,
          stateName: this.stateName,
          zipCode: this.zipCode,
          date: this.dateRequest,
          time: this.time,
          message: this.message,
        })
        // Reset form field
        this.firstName = ''
        this.lastName = ''
        this.phoneNumber = ''
        this.email = ''
        this.streetName = ''
        this.cityName = ''
        this.stateName = ''
        this.zipCode = ''
        this.dateRequest = ''
        this.time = ''
        this.message = ''
      } catch(error) {
        console.log({error})
      }
    //}
    },
  }
};
</script>

<style scoped>
.input-container {
  width: 710px;
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
  background-color: #D8E2DC;
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
  padding-bottom: 40px;
  .v-btn {
    border: 1px solid black;
    background-color: #D8E2DC;
  }
}
.datePicker >>> .mx-input {
  height: 50px;
  border: 1.5px solid black;
  background-color: #D8E2DC;
}
.v-input >>> .v-input__slot::before{
  border-style: none !important;
}
.v-input >>> .v-input__slot::after{
  border-style: none !important;
}
.v-input >>> .v-input__slot > .v-text-field__slot {
  margin-left: 5px;
}
</style>
