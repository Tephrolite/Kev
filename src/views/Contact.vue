<template>
  <v-container style="margin-top: 50px; width: 100%;">
    <v-row d-flex class="pageContainer">      
      <div class="contactDescription">Description of product along with expected pricing.</div>
      <div class="input-container">
        <v-row class="input-content mt-5">
          <v-form id="contactForm">
          <v-row>
            <v-col>
              <p class="mb-0">First Name*</p>
              <v-text-field id="contactFirstName" class="mediumInput" hide-details name="firstName" v-model="firstName" placeholder="John"
              ></v-text-field>
            </v-col>
            <v-col>
              <p>Last Name*</p>
              <v-text-field id="contactLastName" class="mediumInput" name="lastName" v-model="lastName" placeholder="Doe"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <p>Phone Number*</p>
              <v-text-field id="contactPhoneNumber" class="mediumInput" name="phoneNumber" v-model="phoneNumber" placeholder="(###) ###-####"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>              
              <p>Email Address*</p>
              <v-text-field id="contactEmailAddress" class="largeInput" name="email" v-model="email" placeholder="john.doe@email.com"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>            
              <p>What can we help you with?</p>
              <v-textarea id="contactMessage" no-resize class="textArea" name="message" v-model="message" placeholder="Type your message here.."></v-textarea>
            </v-col>
          </v-row>
          <v-row class="submitButton">
            <v-btn @click="sendEmail()">Submit</v-btn>
          </v-row>
        </v-form>
        
      </v-row>
      </div>
    </v-row>
  </v-container>
</template>

<script>
import emailjs from 'emailjs-com';

export default {
  name: "ContactView",

  data: () => ({
    firstName: "",
    lastName: "",
    phoneNumber: "",
    email: "",
    message: "",
  }),
  methods: {
    sendEmail() {
      if (this.firstName == "") {
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
      } else {
      try {
        emailjs.sendForm('service_2grbipg', 'template_tdvdmim', "#contactForm" ,"bJYwKkriG105jLWq8", {
          firstName: this.firstName,
          lastName: this.lastName,
          phoneNumber: this.phoneNumber,
          email: this.email,
          message: this.message,
        })
        // Reset form field
        this.firstName = ''
        this.lastName = ''
        this.phoneNumber = ''
        this.email = ''
        this.message = ''
      } catch(error) {
        console.log({error})
      }
    }
    },
  }
};
</script>

<style scoped>
.pageContainer {
  justify-content: space-between;
  width: 100%;
}
.input-container {
  width: 710px;
  height: 565px;
  background-color: #DCA7A7;
  box-shadow: -10px 10px 2px 0 rgb(115 91 91);
  color: black;
  font-weight: 500;
  float: right;
}
.input-content {
  margin-left: 30px;
  margin-top: 10px;
}
.v-input.v-text-field {
  background-color: #D8E2DC;
  border-style: solid;
  border-radius: 5px;
  padding-left: 5px;
}
.mediumInput {
  width: 312px;
  height: 50px;
}

.largeInput {
  width: 650px;
  height: 50px;
}
.textArea {
  width: 650px;
  height: 150px;
}
.v-input.v-text-field>.v-input__control>.v-text-field__slot {
  max-height: 20px;
}
.contactDescription {
  color: black;
  font-weight: 500;
  margin-left: 20px;
  width: 200px;
}
.submitButton {
  margin-left: 0px;
  .v-btn {
    border: 1px solid black;
    background-color: #D8E2DC;
  }
}
.v-input >>> .v-input__slot::before{
  border-style: none !important;
}
.v-input >>> .v-input__slot::after{
  border-style: none !important;
}
</style>