<template>
  <div class="jumbotron vertical-center">
    <div class="container">
      <div class="row">
        <div class="col-sm-12">
          <h1>Recipes</h1>
          <hr />
          <br />
          <b-alert v-if=showMessage variant="success" show>{{ message }}</b-alert>
          <button type="button" class="btn btn-success btn-sm" v-b-modal.account-modal>
            Add Recipe
          </button>
          <br /><br />
          <table class="table table-hover">
            <thead>
              <tr>
                <th scope="col">Recipe Name</th>
                <th scope="col">Recipe Ingredients</th>
                <th scope="col">Recipe Steps</th>
                <th scope="col">Recipe Rating</th>
                <th scope="col">Recipe Favorite</th>
                <th scope="col">Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="account in accounts" :key="account.id">
                <td>{{ account.name }}</td>
                <td>{{ account.ingredients }}</td>
                <td>{{ account.steps }}</td>
                <td>{{ account.rate}}/5</td>    
                <td>
                   <!--Add a checkbox  -->
                  <b-form-checkbox v-model="account.favorite" disabled ></b-form-checkbox>
                </td>
            
                <td>
                  <div class="btn-group" role="group">
                    <button type="button" class="btn btn-info btn-sm" v-b-modal.edit-account-modal
                      @click="editAccount(account)">
                      Edit
                    </button>
                    <button type="button" class="btn btn-danger btn-sm" @click="deleteAccount(account)">
                      Delete
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Start of Modal for Create Account-->
      <b-modal ref="addAccountModal" id="account-modal" title="Create a new account" hide-backdrop hide-footer>
        <b-form @submit="onSubmit" class="w-100">

          <b-form-group id="form-name-group" label="Recipe Name:" label-for="form-name-input">
            <b-form-input id="form-name-input" type="text" v-model="createAccountForm.name" placeholder="The name of the recipe"
              required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-ingredients-group" label="Ingredients:" label-for="form-ingredients-input">
            <b-form-input id="form-ingredients-input" type="text" v-model="createAccountForm.ingredients" placeholder="The ingredients needed"
              required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-steps-group" label="Steps:" label-for="form-steps-input">
            <b-form-input id="form-steps-input" type="text" v-model="createAccountForm.steps" placeholder="The step-by-step process"
              required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-rate-group" label="Rate 1 to 5:" label-for="form-rate-input">
            <b-form-input id="form-rate-input" type="range" v-model="createAccountForm.rate" min="1" max="5" step="1" 
            required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-favorite-group" label="Favorite:" label-for="form-favorite-input">
            <b-form-checkbox id="form-favorite-input" type="bool" v-model="createAccountForm.favorite" placeholder="Marked as favorite or not">
            </b-form-checkbox>
          </b-form-group>

          <b-button type="submit" variant="outline-info">Submit</b-button>
        </b-form>
      </b-modal>
      <!-- End of Modal for Create Account-->
      <!-- Start of Modal for Edit Account-->
      <b-modal ref="editAccountModal" id="edit-account-modal" title="Edit the account" hide-backdrop hide-footer>
        <b-form @submit="onSubmitUpdate" class="w-100">
          <b-form-group id="form-edit-name-group" label="Recipe Name:" label-for="form-edit-name-input">
            <b-form-input id="form-edit-name-input" type="text" v-model="editAccountForm.name"
              placeholder="Recipe Name" required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-edit-ingredients-group" label="Ingredients:" label-for="form-edit-ingredients-input">
            <b-form-input id="form-edit-ingredients-input" type="text" v-model="editAccountForm.ingredients"
              placeholder="Recipe Ingredients" required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-edit-steps-group" label="Steps:" label-for="form-edit-steps-input">
            <b-form-input id="form-edit-steps-input" type="text" v-model="editAccountForm.steps"
              placeholder="Recipe Steps" required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-edit-rate-group" label="Rate 1 to 5:" label-for="form-edit-rate-input">
            <b-form-input id="form-edit-rate-input" type="range" v-model="editAccountForm.rate" min="1" max="5" step="1" 
            required>
            </b-form-input>
          </b-form-group>

          <b-form-group id="form-edit-favorite-group" label="Favorite:" label-for="form-edit-favorite-input">
            <b-form-checkbox id="form-edit-favorite-input" type="bool" v-model="editAccountForm.favorite"
              placeholder="True/False" required>
            </b-form-checkbox>
          </b-form-group>

          <b-button type="submit" variant="outline-info">Update</b-button>
        </b-form>
      </b-modal>
      <!-- End of Modal for Edit Account-->

    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "AppAccounts",
  data() {
    return {
      accounts: [],
      createAccountForm: {
        name: "",
        ingredients: "",
        steps: "",
        rate: "",
        favorite: false,
      },
      editAccountForm: {
        id: "",
        name: "",
        ingredients: "",
        steps: "",
        rate: "",
        favorite: false,        
      },
      showMessage: false,
      message: "",
    };
  },
  methods: {
    // GET accounts
    getAccounts() {
      const path = `${process.env.VUE_APP_ROOT_URL}`;
      axios
        .get(path)
        .then((response) => {
          this.accounts = response.data.recipes;
          // Print in cççonsole
          // console.log(response.data);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    // POST function
    createAccount(payload) {
      const path = `${process.env.VUE_APP_ROOT_URL}`;
      axios
        .post(path, payload)
        .then((response) => {
          this.getAccounts();
          // For message alert
          this.message = "Recipe Created succesfully!";
          // To actually show the message
          this.showMessage = true;
          // To hide the message after 3 seconds
          setTimeout(() => {
            this.showMessage = false;
          }, 3000);
        })
        .catch((error) => {
          console.error(error);
          this.getAccounts();
        });
    },
    // Update function
    updateAccount(payload, accountId) {

      const path = `${process.env.VUE_APP_ROOT_URL}/${accountId}`;

      console.log(payload);

      axios
        .put(path, payload)
        .then((response) => {
          this.getAccounts();
          // For message alert
          this.message = "Recipe Updated succesfully!";
          // To actually show the message
          this.showMessage = true;
          // To hide the message after 3 seconds
          setTimeout(() => {
            this.showMessage = false;
          }, 3000);
        })
        .catch((error) => {
          console.error(error);
          this.getAccounts();
        });
    },
    // Delete account
    RESTdeleteAccount(accountId) {
      const path = `${process.env.VUE_APP_ROOT_URL}/${accountId}`;
      axios
        .delete(path)
        .then((response) => {
          this.getAccounts();
          // For message alert
          this.message = "Recipe Deleted succesfully!";
          // To actually show the message
          this.showMessage = true;
          // To hide the message after 3 seconds
          setTimeout(() => {
            this.showMessage = false;
          }, 3000);
        })
        .catch((error) => {
          console.error(error);
          this.getAccounts();
        });
    },

    initForm() {
      this.createAccountForm.name = "";
      this.createAccountForm.ingredients = "";
      this.createAccountForm.steps = "";
      this.createAccountForm.rate = "";
      this.createAccountForm.favorite = false;
      
      this.editAccountForm.id = "";
      this.editAccountForm.name = "";
      this.editAccountForm.ingredients = "";
      this.editAccountForm.steps = "";
      this.editAccountForm.rate = "";
      this.editAccountForm.favorite = false;
    },
    onSubmit(e) {
      e.preventDefault(); //prevent default form submit form the browser
      this.$refs.addAccountModal.hide(); //hide the modal when submitted
      const payload = {
        name: this.createAccountForm.name,
        ingredients: this.createAccountForm.ingredients,
        steps: this.createAccountForm.steps,
        rate: this.createAccountForm.rate,
        favorite: this.createAccountForm.favorite,
      };
      this.createAccount(payload);
      this.initForm;
    },
    // Handle submit event for edit account
    onSubmitUpdate(e) {
      e.preventDefault(); //prevent default form submit form the browser
      this.$refs.editAccountModal.hide(); //hide the modal when submitted
      const payload = {
        name: this.editAccountForm.name,
        ingredients: this.editAccountForm.ingredients,
        steps: this.editAccountForm.steps,
        rate: this.editAccountForm.rate,
        favorite: this.editAccountForm.favorite,
      };
      this.updateAccount(payload, this.editAccountForm.id);
      this.initForm;
    },
    //Prepare edit account form with the name of the account
    editAccount(account) {
      this.editAccountForm = account;
    },
    // Handle Delete button
    deleteAccount(account) {
      this.RESTdeleteAccount(account.id);
    },
  },
  created() {
    this.getAccounts();
  },
};
</script>
