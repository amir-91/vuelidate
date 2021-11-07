<template>
    <div class="jumbotron">
        <div class="container">
            <div class="row">
                <div class="col-sm-8 offset-sm-2">
                    <div>
                        <h2>Contact Us</h2>
                        <form @submit.prevent="handleSubmit">
                            <div class="form-group">
                                <label for="Name">Name</label>
                                <input v-model="user.Name" id="Name" name="Name" class="form-control" :class="{ 'is-invalid': submitted && $v.user.Name.$error }" />
                                <div v-if="submitted && $v.user.Name.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.Name.required">Name is required</span>
                                    <span v-if="!$v.user.Name.alpha">Must be letters only</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="mobile">Mobile number</label>
                                <input v-model="user.mobile" id="mobile" name="mobile" class="form-control" :class="{ 'is-invalid': submitted && $v.user.mobile.$error }" />
                                <div v-if="submitted && $v.user.mobile.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.mobile.required">Mobile is required</span>
                                    <span v-if="!$v.user.mobile.numeric">Must be numbers only</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="email">Email</label>
                                <input v-model="user.email" id="email" name="email" class="form-control" :class="{ 'is-invalid': submitted && $v.user.email.$error }" />
                                <div v-if="submitted && $v.user.email.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.email.required">Email is required</span>
                                    <span v-if="!$v.user.email.email">Email is invalid</span>
                                </div>
                            </div>
                             <div class="form-group">
                                <label for="nationality">Nationality</label>
                                <select name="nationality" v-model="user.nationality" id="nationality" class="form-control" :class="{ 'is-invalid': submitted && $v.user.nationality.$error }">
                                     <option value="">-- select one --</option>
                                     <option value="afghan">Afghan</option>
                                     <option value="albanian">Albanian</option>
                                     <option value="algerian">Algerian</option>
                                     <option value="american">American</option>
                                     <option value="andorran">Andorran</option>
                                     <option value="angolan">Angolan</option>
                                     <option value="antiguans">Antiguans</option>
                                     <option value="argentinean">Argentinean</option>
                                     <option value="armenian">Armenian</option>
                                     <option value="australian">Australian</option>
                                     <option value="austrian">Austrian</option>
                                     <option value="azerbaijani">Azerbaijani</option>
                                     <option value="bahamian">Bahamian</option>
                                     <option value="bahraini">Bahraini</option>
                                     <option value="bangladeshi">Bangladeshi</option>
                                     <option value="barbadian">Barbadian</option>
                                     <option value="barbudans">Barbudans</option>
                                     <option value="batswana">Batswana</option>
                                     <option value="belarusian">Belarusian</option>
                                 </select>
                                <div v-if="submitted && $v.user.nationality.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.nationality.required">nationality is required</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="email">Message</label>
                                <textarea name="textarea" rows="6" v-model="user.textarea" id="textarea" class="form-control" :class="{ 'is-invalid': submitted && $v.user.textarea.$error }"/>
                                <div v-if="submitted && $v.user.textarea.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.textarea.required">This field is required</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <button class="btn btn-primary">Register</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { required, email, numeric, alpha } from "vuelidate/lib/validators";

    export default {
        name: "app",
        data() {
            return {
                user: {
                    Name: "",
                    mobile: "",
                    email: "",
                    nationality: "",
                    textarea: ""
                },
                submitted: false
            };
        },
        validations: {
            user: {
                Name: { required, alpha },
                mobile: { required, numeric },
                nationality: { required },
                email: { required, email },
                textarea: { required }
            }
        },
        methods: {
            handleSubmit() {
                this.submitted = true;

                // stop here if form is invalid
                this.$v.$touch();
                if (this.$v.$invalid) {
                    return;
                }

                alert("SUCCESS!! :-)\n\n" + JSON.stringify(this.user));
            }
        }
    };
</script>