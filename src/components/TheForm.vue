<template>
    
    <form @submit.prevent="submitForm">
        <div class="form-group" :class="{invalid: userNameValidity === 'invalid'}">
            <label for="user-name">Name</label>
            <!-- blur fires when the element has lost focus -->
            <input type="text" class="form-control" id="user-name" name="user-name" v-model.trim="userName" @blur="validateInput">
            <p v-if="userNameValidity ==='invalid'">Please enter a valid name!</p>
        </div>   
        <!-- ref converts value to string v-model does not -->
        <div class="form-control">
            <label for="age">Age</label>
            <input type="number" class="form-control" id="age" name="age" v-model="userAge" ref="ageInput">
        </div>
        <!-- set default value in data -->
        <div class="form-control">
            <label for="referrer">How did you hear about us?</label>
            <select id="referrer" name="referrer" v-model="refferrer">
                <option value="google">Google</option>
                <option value="wom">Word of mouth</option>
                <option value="other">Other</option>
            </select>
        </div>
        <!-- checkboxes are saved in an array -->
        <div class="form-control">
            <h2>What are you interested in?</h2>
            <div>
                <input id="interest-news" name="interest" type="checkbox" value="news" v-model="interests" />
                <label for="interest-news">News</label>
            </div>
            <div>
                <input
                id="interest-tutorials"
                name="interest"
                type="checkbox"
                value="tutorials"
                v-model="interests"
                />
                <label for="interest-tutorials">Tutorials</label>
            </div>
            <div>
                <input
                id="interest-nothing"
                name="interest"
                type="checkbox"
                value="nothing"
                v-model="interests"
                />
                <label for="interest-nothing">Nothing</label>
            </div>
        </div>
        <div class="form-control">
          <h2>How do you learn?</h2>
          <div>
            <input id="how-video" name="how" type="radio" value="video" v-model="how" />
            <label for="how-video">Video Courses</label>
          </div>
          <div>
            <input id="how-book" name="how" type="radio" value="book" v-model="how" />
            <label for="how-book">Books</label>
          </div>
          <div>
            <input id="how-both" name="how" type="radio" value="both" v-model="how" />
            <label for="how-both">Both</label>
          </div>
        </div>
        <!-- use v-model on component -->
        <div class="form-control">
            <h2>How do you rate our service?</h2>
            <rating-control v-model="rating"></rating-control>
        </div>
        <div class="form-control">
          <input type="checkbox" id="confirm-terms" name="confirm-terms" v-model="confirm" />
          <label for="confirm-terms">Agree to terms of use?</label>
        </div>


        <button type="submit">save data</button>
    </form>

</template>

<script>

import RatingControl from './RatingControl.vue';

    export default {
        data(){
            return {
                userName: '',
                userAge: null,
                userNameValidity: 'pending',
                refferrer: 'wom',
                interests: [],
                how: null,
                rating: null,
                confirm: false
            }
        },
        components: {RatingControl},
        methods: {
            submitForm(){
                console.log('Username: ' +this.userName);
                // resetting username
                this.userName = '';
                console.log('User age: ');
                console.log(this.userAge + 5);
                console.log(this.$refs.ageInput.value + 5);
                this.userAge = null;
                console.log('Referrer: ' +this.refferrer);
                this.refferrer = 'wom';
                console.log('Checkboxes:')
                console.log('Interests: ' +this.interests);
                this.interests = [];
                console.log('Radio buttons');
                console.log(this.how);
                this.interest = [];
                this.how = null;
                console.log('Rating: ' +this.rating);
                this.rating = null;
                console.log('Confirm: ' +this.confirm);
                this.confirm = false;

                
            },
            validateInput(){
               if(this.userName ===''){
                this.userNameValidity = 'invalid';
               } else {
                this.userNameValidity = 'valid';
               }
               console.log('Username validity: ' +this.userNameValidity);
            }
        }
    }


</script>


<style scoped>

form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}

</style>