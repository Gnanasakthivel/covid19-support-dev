<template>
  <div>
    <div class="container mt-4">
      <div class="animated fadeIn">
        <div class="row">
          <div class="col-sm-12">
            <div class="card">
              <div class="card-body">
                <div class="row">
                  <div class="col-sm-12">
                    <h4 class="mb-4 text-primary">What support you need?</h4>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-4">
                    <fieldset role="group" class="b-form-group form-group-cat">
                      <div role="group" class>
                        <b-form-group label="Category of the support" label-for="basicSelect" :label-cols="6">
                        <b-form-select
                          id="basicSelect"
                          :plain="true" 
                          :options="donation_categories"
                          value="Please select"
                          v-model="form.request.category"
                        ></b-form-select>
                      </b-form-group>
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-8">
                    <fieldset role="group" class="b-form-group form-group-cat">
                      <div role="group" class>
                        <input
                          id="helptitle"
                          type="text"
                          placeholder="Short intro of what type of support need"
                          class="form-control"
                          v-model="form.request.title"
                        />
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-12">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <textarea
                          id="helptitle"
                          type="text"
                          placeholder="Description of what you need"
                          class="form-control"
                          rows="3"
                          v-model="form.request.detail"
                        />
                      </div>
                    </fieldset>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-sm-12">
            <div class="card">
              <div class="card-header">
                <div>
                  <strong>Requestor details</strong>
                </div>
              </div>
              <div class="card-body">
                <div class="row">
                  <div class="col-sm-12">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="requestfor">Requesting for</label>
                        <div id="requestfor" role="radiogroup" tabindex="-1" class>
                          <div class="custom-control custom-radio custom-control-inline">
                            <input
                              type="radio"
                              id="requestfor1"
                              name="requestfor"
                              value="self"
                              checked="checked"
                              class="custom-control-input"
                              v-model="form.requesting_for"
                            />
                            <label for="requestfor1" class="custom-control-label">Self</label>
                          </div>
                          <div class="custom-control custom-radio custom-control-inline">
                            <input
                              type="radio"
                              id="requestfor2"
                              name="requestfor"
                              value="other"
                              class="custom-control-input"
                              v-model="form.requesting_for"
                            />
                            <label for="requestfor2" class="custom-control-label">On behalf others</label>
                          </div>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-sm-12">
            <div class="card">
              <div class="card-header">
                <div>
                  <strong>Details of person requiring support</strong>
                </div>
              </div>
              <div class="card-body">
                <div class="row">
                  <div class="col-sm-12">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="fullname">Full Name</label>
                        <input
                          id="fullname"
                          type="text"
                          placeholder="Full name of the person required support"
                          class="form-control"
                          v-model="form.contact.name"
                          :class="{ 'is-invalid': submitted && $v.form.contact.name.$error }"
                        />
                        <div v-if="submitted && $v.form.contact.name.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.name.required">Name is required</span>
							                <span v-if="(!$v.form.contact.name.validName) && ($v.form.contact.name.required)">Name is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="phonenumber">Phone Number</label>
                        <input
                          id="phonenumber"
                          type="text"
                          placeholder="Phone number"
                          class="form-control"
                          v-model="form.contact.phone"
                          :class="{ 'is-invalid': submitted && $v.form.contact.phone.$error }"
                        />
                        <div v-if="submitted && $v.form.contact.phone.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.phone.required">Phone Numer is required</span>
							                <span v-if="(!$v.form.contact.phone.validPhoneNo) && ($v.form.contact.phone.required)">Phone Numer is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="email">Email</label>
                        <input
                          id="email"
                          type="text"
                          placeholder="Email"
                          class="form-control"
                          v-model="form.contact.email"
                          :class="{ 'is-invalid': submitted && $v.form.contact.email.$error }" 
                        />
                        <div v-if="submitted && $v.form.contact.email.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.email.required">Email is required</span>
                              <span v-if="!$v.form.contact.email.email">Email is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
			          <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="address">Address</label>
                        <input
                          id="houseNo"
                          type="text"
                          placeholder="House Number"
                          class="form-control"
                          v-model="form.contact.houseNo"
                          :class="{ 'is-invalid': submitted && $v.form.contact.houseNo.$error }" 
                        />
                        <div v-if="submitted && $v.form.contact.houseNo.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.houseNo.required">Valid House Number is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <div class="marginPadding"></div>
                        <input
                          id="streetName"
                          type="text"
                          placeholder="Street Name"
                          class="form-control"
                          v-model="form.contact.streetName"
                          :class="{ 'is-invalid': submitted && $v.form.contact.streetName.$error }" 
                        />
                        <div v-if="submitted && $v.form.contact.streetName.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.streetName.required">Street Name is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="city"
                          type="text"
                          placeholder="City/Area"
                          class="form-control"
                          v-model="form.contact.city" 
                        />
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="country"
                          type="text"
                          placeholder="Country"
                          class="form-control"
                          v-model="form.contact.country" 
                        />
                         <vue-modaltor  :visible="open" @hide="hideModal">
                              <div v-if="error" class="alert alert-danger">{{error}}</div>
                              <div v-if="(status==='submitted' || status==='new')" class="alert alert-success">Your request (Id: {{form.requestId}}) created successfully</div>
                         </vue-modaltor>
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="postCode"
                          type="text"
                          placeholder="Postal Code"
                          class="form-control"
                          v-model="form.contact.postCode"
                          :class="{ 'is-invalid': submitted && $v.form.contact.postCode.$error }" 
                        />
                        <div v-if="submitted && $v.form.contact.postCode.$error" class="invalid-feedback">
                              <span v-if="!$v.form.contact.postCode.required">Postcode is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
                
              </div>
            </div>
          </div>
        </div>
        <div class="row" v-if="form.requesting_for === 'other'">
          <div class="col-sm-12">
            <div class="card">
              <div class="card-header">
                <div>
                  <strong>Details of person submitting request</strong>
                </div>
              </div>
              <div class="card-body">
                <div class="row">
                  <div class="col-sm-12">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="fullname">Full Name</label>
                        <input
                          id="fullname"
                          type="text"
                          placeholder="Full name of the person required support"
                          class="form-control"
                          v-model="form.requestor.name"
                          :class="{ 'is-invalid': submitted  && submittedOther && $v.form.requestor.name.$error }"
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.name.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.name.required">Name is required</span>
							                <span v-if="(!$v.form.requestor.name.validName) && ($v.form.requestor.name.required)">Name is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="phonenumber">Phone Number</label>
                        <input
                          id="phonenumber"
                          type="text"
                          placeholder="Phone number"
                          class="form-control"
                          v-model="form.requestor.phone"
                          :class="{ 'is-invalid': submitted && submittedOther && $v.form.requestor.phone.$error }"
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.phone.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.phone.required">Phone Numer is required</span>
							                <span v-if="(!$v.form.requestor.phone.validPhoneNo) && ($v.form.requestor.phone.required)">Phone Numer is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="email">Email</label>
                        <input
                          id="email"
                          type="text"
                          placeholder="Email"
                          class="form-control"
                          v-model="form.requestor.email"
                          :class="{ 'is-invalid': submitted && submittedOther && $v.form.requestor.email.$error }" 
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.email.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.email.required">Email is required</span>
                              <span v-if="!$v.form.requestor.email.email">Email is invalid</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
			          <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <label for="address">Address</label>
                        <input
                          id="houseNo"
                          type="text"
                          placeholder="House Number"
                          class="form-control"
                          v-model="form.requestor.houseNo"
                          :class="{ 'is-invalid': submitted && submittedOther && $v.form.requestor.houseNo.$error }" 
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.houseNo.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.houseNo.required">Valid House Number is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <div class="marginPadding"></div>
                        <input
                          id="streetName"
                          type="text"
                          placeholder="Street Name"
                          class="form-control"
                          v-model="form.requestor.streetName"
                          :class="{ 'is-invalid': submitted && submittedOther && $v.form.requestor.streetName.$error }" 
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.streetName.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.streetName.required">Street Name is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="city"
                          type="text"
                          placeholder="City/Area"
                          class="form-control"
                          v-model="form.requestor.city" 
                        />
                      </div>
                    </fieldset>
                  </div>
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="country"
                          type="text"
                          placeholder="Country"
                          class="form-control"
                          v-model="form.requestor.country" 
                        />
                      </div>
                    </fieldset>
                  </div>
                </div>
                <div class="row">
                  <div class="col-sm-6">
                    <fieldset role="group" class="b-form-group form-group">
                      <div role="group" class>
                        <input
                          id="postCode"
                          type="text"
                          placeholder="Postal Code"
                          class="form-control"
                          v-model="form.requestor.postCode"
                          :class="{ 'is-invalid': submitted && submittedOther && $v.form.requestor.postCode.$error }" 
                        />
                        <div v-if="submitted && submittedOther && $v.form.requestor.postCode.$error" class="invalid-feedback">
                              <span v-if="!$v.form.requestor.postCode.required">Postcode is required</span>
                        </div>
                      </div>
                    </fieldset>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-sm-12">
            <div class="card">
              <div class="card-body">
                <div class="row">
                  <div class="col-sm-8">
                    <div>
                      <p>By submitting, I am agreeing the T&C and sharing all the above information with the support team.</p>
                    </div>
                  </div>
                  <div class="col-sm-4">
                    <div class="text-right mr-4" v-if="!requestStatus" >
                      <button
                        type="button"
                        class="btn btn-primary"
                        @click="submitRequest"
                      >Agree & Submit Request</button>
                    </div>
                    <div class="text-right mr-4" v-if="requestStatus" >
                      <button
                        type="button"
                        class="btn btn-primary"
                      >Loading...</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase";
import { mapGetters } from "vuex";
import axios from "axios";
import { required, email, numeric } from "vuelidate/lib/validators";

const validName = function (name) {
    name=name.trim();
    return (name.length >= 2 && /^(?=.{1,50}$)[a-z]+(?:['_.\s][a-z]+)*$/i.test(name));
}

const validPhoneNo = function (phone) {
    return (/^[\+]?[(]?[0-9]{3}[)]?[-\s\.]?[0-9]{3}[-\s\.]?[0-9]{4,6}$/im.test(phone));
}

export default {
  data() {
    return {
      shouldDisabled: false,
      submitted: false,
      submittedOther: false,
      validateSelfAlone: false,
      requestId:"",
      requestStatus: false,
      open: false,
      donation_categories: [
        "General",
        "Food",
        "Groceries",
        "Toys",
        "Books",
        "Furniture",
        "Cloths",
        "Medical supplies",
        "Electronics",
        "Other"
      ],
      form: {
        request: {
          category: "General",
          title: "",
          detail: "",
          status: "new"
        },
        requestId:"",
        picked_up_by: "",
        picked_up_on: new Date(),
        assigned_groups: [],
        tags: [],
        requesting_for: "self",
        contact: {
          name: "",
          address: "",
          phone: "",
          email: "",
          houseNo: "",
          streetName: "",
          address: "",
          country: "",
          postCode: "",
          city:""
        },
        requestor: {
          name: "",
          address: "",
          phone: "",
          email: "",
          houseNo: "",
          streetName: "",
          address: "",
          country: "",
          postCode: "",
          city:""
        }
      },
      error: null,
      status: "new"
    };
  },
  computed: {
    ...mapGetters({
      user: "user"
    })
  },
  validations: {
         form: {
            contact: {
                email: { required, email },
                name: { required, validName},
                phone: { required, validPhoneNo },
                houseNo: { required },
                streetName: { required },
                postCode: {required}            
             },
             requestor: {
                email: { required, email },
                name: { required, validName},
                phone: { required, validPhoneNo },
                houseNo: { required },
                streetName: { required },
                postCode: {required}                    
             }
         }    
  },
  methods: {
    hideModal() {
              this.open = false
    },
    submitRequest() {
      this.submitted = true;

      if(this.form.requesting_for === 'other') {
          this.submittedOther=true;
          this.validateSelfAlone=this.$v.form.requestor.$invalid;
          this.form.requestor.address=this.form.requestor.houseNo+", "+this.form.requestor.streetName;
          this.form.requestor.name=this.form.requestor.name.trim();
      } else {
          this.submittedOther=false;
          this.validateSelfAlone=false;
          this.form.contact.address=this.form.contact.houseNo+", "+this.form.contact.streetName;
          this.form.contact.name=this.form.contact.name.trim();
      }
      
      // stop here if form is invalid
      this.$v.$touch();
      if (this.$v.form.contact.$invalid || this.validateSelfAlone) {
         return;
      }

      this.requestStatus=true;

      if (this.user.loggedIn && this.user.data) {
        this.form.user_displayName =
          this.user.data.displayName || this.user.data.email;
        this.form.user_email = this.user.data.email;
      }

      this.form.verified = false;
      this.form.upvotes = [];
      this.form.downvotes = [];
      this.form.timestamp = new Date();
     var db = firebase.firestore();
     db.collection("support_requests")
        .add(this.form)
        .then(docRef => {
          this.status = "submitted";
          this.error = null;
          this.form.requestId=docRef.id;
          this.open = true;
          this.requestStatus=false;
          setTimeout(() => {
            this.status = "new";
            this.error = null;
          }, 5 * 1000);
        })
        .catch(error => {
          this.error = error;
          this.status = "error";
          this.requestId="";
          this.requestStatus=false;
        });
    }
  }
};

</script>

<style>
.marginPadding {
   margin-bottom: 1.79rem !important;
}

.form-group-cat {
    margin-bottom: 0.5rem !important;
}

.modal-vue--content {
    background-color: rgb(240, 243, 245);
    background-clip: border-box;
    border: 1px solid #c8ced3;
    border-radius: 0.25rem;
}

.modal-vue--content-panel {
    margin-top: 1.5rem !important;
    margin-left: 1.5rem !important;
    margin-right: 1.5rem !important;
    margin-bottom: 0.25rem !important;
}

.modal-vue-overlay {
  opacity: 0.5;
}

</style>