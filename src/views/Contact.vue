<template>
  <v-container style="margin-top: 50px; width: 100%;">
    <v-row d-flex class="pageContainer">      
      <div class="contactDescription">Description of product along with expected pricing.</div>
      <div class="input-container">
        <v-row class="input-content mt-5">
          <v-form v-model="contact" id="contactForm">
          <v-row>
            <v-col>
              {{ this.name }}
              <p class="mb-0">First Name*</p>
              <v-text-field class="mediumInput" hide-details name="firstName" v-model="firstName"
              ></v-text-field>
            </v-col>
            <v-col>
              <p>Last Name*</p>
              <v-text-field class="mediumInput" name="lastName" v-model="lastName"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>
              <p>Phone*</p>
              <v-text-field class="mediumInput" name="phoneNumber" v-model="phoneNumber"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>              
              <p>Email*</p>
              <v-text-field class="largeInput" name="email" v-model="email"></v-text-field>
            </v-col>
          </v-row>
          <v-row>
            <v-col>            
              <p>What can we help you with?</p>
              <v-textarea no-resize class="textArea" name="message" v-model="message"></v-textarea>
            </v-col>
          </v-row>
          <v-row class="submitButton">
            <v-btn @click="sendEmail()">Submit</v-btn>
            <input type="submit" value="Send">
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
      try {
        emailjs.sendForm('service_2grbipg', 'template_tdvdmim', "#contactForm" ,"bJYwKkriG105jLWq8", {
          firstName: this.firstName,
          lastName: this.lastName,
          phoneNumber: this.phoneNumber,
          email: this.email,
          message: this.message,
        })
      } catch(error) {
        console.log({error})
      }
      console.log(this.message)
      // Reset form field
      this.firstName = ''
      this.lastName = ''
      this.phoneNumber = ''
      this.email = ''
      this.message = ''
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
  }
}
</style>