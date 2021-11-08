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
                                <input v-model="user.englishName" id="english-name" name="Name" class="form-control" :class="{ 'is-invalid': submitted && $v.user.englishName.$error }" />
                                <div v-if="submitted && $v.user.englishName.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.englishName.required">Name is required</span>
                                    <span v-if="!$v.user.englishName.alpha">Must be english letters only</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="Name">الاسم</label>
                                <input v-model="user.arabicName" id="arabic-name" name="Name" class="form-control" :class="{ 'is-invalid': submitted && $v.user.arabicName.$error }" />
                                <div v-if="submitted && $v.user.arabicName.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.arabicName.required">الاسم مطلوب</span>
                                    <span v-if="!$v.user.arabicName.arabicAlpha">يجب ان يحتوى على حروف عربى فقط</span>
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
                                <select name="nationality" @input="reset" v-model="user.nationality" id="nationality" class="form-control" :class="{ 'is-invalid': submitted && $v.user.nationality.$error }">
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
                                     <option value="Egypt">Egypt</option>
                                 </select>
                                <div v-if="submitted && $v.user.nationality.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.nationality.required">nationality is required</span>
                                </div>
                            </div>
                             <div v-if="user.nationality === 'Egypt'" class="form-group">
                                <label for="nationalId">National ID</label>
                                <input v-model="user.nationalId" id="nationalId" name="nationalId" class="form-control" :class="{ 'is-invalid': submitted && $v.user.nationalId.$error }" />
                                <div v-if="submitted && $v.user.nationalId.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.nationalId.required">national Id is required</span>
                                    <span v-if="!$v.user.nationalId.numeric">Must be numbers only</span><br>
                                    <span v-if="!$v.user.nationalId.maxLength || !$v.user.nationalId.minLength">Must be 14 digits</span>
                                </div>
                            </div>
                             <div v-if="user.nationality !== 'Egypt' && user.nationality !== ''" class="form-group">
                                <label for="passportNumber">Passport number</label>
                                <input v-model="user.passportNumber" id="passportNumber" name="passportNumber" class="form-control" :class="{ 'is-invalid': submitted && $v.user.passportNumber.$error }" />
                                <div v-if="submitted && $v.user.passportNumber.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.passportNumber.required">Passport number is required</span>
                                    <span v-if="!$v.user.passportNumber.numeric">Must be numbers only</span>
                                </div>
                            </div>
                             <div class="form-group">
                                <label for="password">Password</label>
                                <input type="password" v-model="user.password" id="password" name="password" class="form-control" :class="{ 'is-invalid': submitted && $v.user.password.$error }" />
                                <div v-if="submitted && $v.user.password.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.password.required">Password is required</span>
                                    <span v-if="!$v.user.password.minLength">Password must be at least 6 characters</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="confirmPassword">Confirm Password</label>
                                <input type="password" v-model="user.confirmPassword" id="confirmPassword" name="confirmPassword" class="form-control" :class="{ 'is-invalid': submitted && $v.user.confirmPassword.$error }" />
                                <div v-if="submitted && $v.user.confirmPassword.$error" class="invalid-feedback">
                                    <span v-if="!$v.user.confirmPassword.required">Confirm Password is required</span>
                                    <span v-else-if="!$v.user.confirmPassword.sameAsPassword">Passwords must match</span>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="image">Attach photo</label>
                                <input type="file" @change="onImageChange" id="image" name="image" class="form-control" :class="{ 'is-invalid': submitted && $v.image.$error || imageFlag || imgExt }" />
                                <div v-if="submitted || $v.image.$error || imgExt || imageFlag " class="invalid-feedback">
                                    <span v-if="!$v.image.required">Photo is required</span>
                                    <span v-if="imgExt">accept png or jpeg only</span> <br>
                                    <span v-if="imageFlag">5 mega only</span>
                                </div>
                            </div>
                              <div class="form-group">
                                <label for="pdf">Attach file</label>
                                <input type="file" @change="onFileChange" id="pdf" name="pdf" class="form-control" :class="{ 'is-invalid': submitted && $v.pdf.$error || pdfFlag || pdfExt }" />
                                <div v-if="submitted || $v.pdf.$error || pdfFlag || pdfExt" class="invalid-feedback">
                                    <span v-if="!$v.pdf.required">File is required</span>
                                    <span v-if="pdfExt">accept pdf only</span> <br>
                                    <span v-if="pdfFlag">5 mega only</span>
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
    import { required, email, numeric, alpha, minLength, sameAs, maxLength, helpers, requiredIf } from "vuelidate/lib/validators";
    const arabicAlpha = helpers.regex('alpha', /^[\u0621-\u064A\040]+$/)

    export default {
        name: "app",
        data() {
            return {
                user: {
                    englishName: "",
                    arabicName: "",
                    mobile: "",
                    email: "",
                    nationality: "",
                    textarea: "",
                    password: "",
                    confirmPassword: "",
                    nationalId: "",
                    passportNumber: "",
                },
                submitted: false,
                image: "",
                pdf: "",
                imageSize: 0,
                pdfSize: 0,
                imageFlag: false,
                pdfFlag: false,
                imageExtension: "",
                pdfExtension: "",
                imgExt: false,
                pdfExt: false
            };
        },
        validations: {
            user: {
                englishName: { required, alpha },
                arabicName: { required, arabicAlpha },
                mobile: { required, numeric },
                nationality: { required },
                email: { required, email },
                textarea: { required },
                password: { required, minLength: minLength(6) },
                confirmPassword: { required, sameAsPassword: sameAs('password') },
                nationalId: { 
                    required: requiredIf(function () {
                        const req = this.$v.user.nationality.$model === 'Egypt'
                        return req
                    }),
                    numeric, 
                    minLength: minLength(14), 
                    maxLength: maxLength(14) 
                    },
                passportNumber: { 
                    required: requiredIf(function() {
                        const req = this.$v.user.nationality.$model !== 'Egypt'
                        return req
                    }),
                    numeric 
                    },
            },
            image: { required },
            pdf: { required }
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
            },
            onImageChange(e) {
              const files = e.target.files || e.dataTransfer.files;
              this.imageSize =files[0].size
              this.imageExtension=files[0].type.split('/')[1]
              console.log(this.imageExtension)
              if (!files.length)
                return;
              this.createImage(files[0]);
              if (this.imageSize > 500000) {
                    this.imageFlag = true
                } else {
                    this.imageFlag = false
                }
              if (this.imageExtension !== 'jpeg') {
                  this.imgExt = true
              } else {
                  this.imgExt = false
              }
              console.log(this.imgExt)
            },
             onFileChange(e) {
              const files = e.target.files || e.dataTransfer.files;
              this.fileSize =files[0].size
              this.pdfExtension=files[0].type.split('/')[1]
              console.log(this.pdfExtension)
              if (!files.length)
                return;
              this.createFile(files[0]);
              if (this.fileSize > 500000) {
                    this.pdfFlag = true
                } else {
                    this.pdfFlag = false
                }
              if (this.pdfExtension !== 'pdf') {
                  this.pdfExt = true
              } else {
                  this.pdfExt = false
              }
            }, 
            createImage(file) {
              const reader = new FileReader();
              const vm = this;

              reader.onload = (e) => {
                vm.image = e.target.result;
              };
              reader.readAsDataURL(file);
            },
             createFile(file) {
              const reader = new FileReader();
              const vm = this;

              reader.onload = (e) => {
                vm.pdf = e.target.result;
              };
              reader.readAsDataURL(file);
            },
            reset() {
                this.user.passportNumber = "",
                this.user.nationalId = ""
            },
         }
        }
</script>