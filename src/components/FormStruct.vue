<template>
    <!-- Strucuture Form container -->
    <div class="flex justify-center">
        <LinkCssAwm />

        <!-- Section -->
        <div v-if="section === 1" class="w-11/12 bg-slate-200 rounded-lg flex flex-col h-full">
            <form @submit.prevent="contact">
                <!-- Row container -->
                <div class="flex-grow flex flex-row justify-evenly py-2.5 flex-wrap">
                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label for="country">Pais:</label>
                        <div class="flex items-baseline">
                            <select v-model="country"
                                class="select text-base h-8  border overflow-y-scroll rounded-md max-w-4xl w-2/5 min-w-full"
                                id="country" required @blur="checkCountry">
                                <option value="">Selecciona un país</option>
                                <option v-for="(country, index) in countries" :key="index" :value="country.name">
                                    {{ country.name }}</option>
                            </select>

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="country === ''">
                                    <i v-show="showMessageC" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageC" :fieldValue="country"
                            errorMessage="Por favor selecciona tu país."
                            successMessage="¡Genial, has seleccionado tu país!">
                        </FieldMessage>
                    </div>
                    <!-- Field -->
                    <div class="py-2.5 flex flex-col  w-80">
                        <label class="form-label" for="gender">Género:</label>
                        <div class="flex items-baseline">
                            <select v-model="gender" class="text-base h-8 form-select rounded-md max-w-7xl w-3/6 min-w-full"
                                id="gender" required @blur="checkGender">
                                <option value="">Selecciona tu género</option>
                                <option value="Hombre">Hombre</option>
                                <option value="Mujer">Mujer</option>
                                <option value="Prefiero no especificar">Prefiero no especificar</option>
                            </select>

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="gender === ''">
                                    <i v-show="showMessageG" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageG" :fieldValue="gender"
                            errorMessage="Por favor selecciona tu género."
                            successMessage="¡Genial, has seleccionado tu género!">
                        </FieldMessage>
                    </div>
                </div>

                <!-- Container row Name Lastname -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="name">Nombre:</label>
                        <div class="flex items-baseline">
                            <input v-model="name" class="text-base h-8 form-input rounded-md max-w-7xl w-3/6 min-w-full"
                                type="text" id="name" required placeholder="Escribe tu nombre" @blur="checkName">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="name === ''">
                                    <i v-show="showMessageN" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>
                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageN" :fieldValue="name"
                            errorMessage="Por favor escribe tu nombre ." successMessage="¡Genial!">
                        </FieldMessage>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="lastName">Apellido:</label>
                        <div class="flex items-baseline">
                            <input v-model="lastname"
                                class="text-base h-8 text-slate-400 form-input rounded-md max-w-7xl w-3/6 min-w-full"
                                type="text" id="lastname" required placeholder="Escribe tu apellido" @blur="checkLastname">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="lastname === ''">
                                    <i v-show="showMessageL" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageL" :fieldValue="lastname"
                            errorMessage="Por favor escribe tu apellido." successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                </div>

                <!-- Container row country birthday idNumber -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="birthday">Fecha de Nacimiento:</label>
                        <div class="flex items-baseline">
                            <flat-pickr
                                class="text-base h-8 text-slate-400 form-select rounded-md max-w-7xl w-3/6 min-w-full"
                                v-model="date" id="birthday" :options="options" @blur="checkAge" />

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="birthday === ''">
                                    <i v-show="showMessage" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i v-if="isValidDate" class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Validate and show the message -->
                        <div class="text-sm">
                            <span v-show="showMessage && !isValidDate" class="text-red-500">Debes ser mayor de 18
                                años</span>
                            <span v-show="showMessage && isValidDate" class="text-green-500">¡Genial!</span>
                        </div>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="idNumber">Identificación:</label>
                        <div class="flex items-baseline">
                            <input v-model.number="idNumber"
                                class="text-base h-8 text-slate-400 form-input rounded-md max-w-7xl w-3/6 min-w-full"
                                type="number" id="idNumber" required placeholder="Escribe tu identificación"
                                @blur="checkIdNumber">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="idNumber === ''">
                                    <i v-show="showMessageID" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageID" :fieldValue="idNumber"
                            errorMessage="Por favor digita tu número de Id, debe ser mayor de 5 digitos"
                            successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                </div>

                <!-- Container row Documnet file -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="imageFront">Foto documento frontal:</label>
                        <div class="flex items-baseline">
                            <input v-on:change="onFileSelect" class="form-input" type="file" id="imageFront" required
                                accept=".jpg" placeholder="Imagen frontal en formato jpg" @change="checkImageFront">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="!imageFront">
                                    <i v-show="showMessageIF" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageIF" :fieldValue="imageFront"
                            errorMessage="Por favor selecciona la imagen frontal de tu Id" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="imageBack">Foto documento reverso:</label>
                        <div class="flex items-baseline">
                            <input v-on:change="onFileSelect2" class="form-input" type="file" id="imageBack" required
                                accept=".jpg" placeholder="Imagen reverso en formato jpg" @change="checkImageBack">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="!imageBack">
                                    <i v-show="showMessageIB" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageIB" :fieldValue="imageBack"
                            errorMessage="Por favor selecciona la imagen de atras de tu Id" successMessage="¡Genial!">
                        </FieldMessage>

                    </div>
                </div>
            </form>

            <!-- Buttons section -->
            <div class="flex justify-center py-16">
                <button class="m-0  bg-stone-800 rounded-lg text-white px-6" @click="goToSection(2)">Siguiente</button>
            </div>

        </div>

        <!-- Section -->
        <div v-if="section === 2" class="w-11/12 bg-slate-300 rounded-lg flex flex-col h-full">
            <form @submit.prevent="contact">
                <!-- Row container -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label for="email">Email:</label>
                        <div class="flex items-baseline">
                            <input v-model="email"
                                class="form-input text-base h-8 text-slate-400  rounded-md max-w-7xl w-3/6 min-w-full"
                                type="email" id="email" reuired placeholder="Escribe tu email" @blur="checkEmail">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="email === ''">
                                    <i v-show="showMessageEM" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageEM" :fieldValue="email"
                            errorMessage="Por favor ingresa tu email" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="Password">Contraseña:</label>
                        <div class="flex items-baseline">
                            <input v-model="password"
                                class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full"
                                type="password" id="password" required placeholder="Escribe tu contraseña" @blur="checkPassword">
                            
                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="password === ''">
                                    <i v-show="showMessagePS" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessagePS" :fieldValue="password"
                            errorMessage="Por favor ingresa tu contraseña" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                </div>


                <!-- Container row confirm password, phonenumber movilNumber -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="confirmPassword">Confirmar contraseña:</label>
                        <div class="flex items-baseline">
                            <input v-model="confirmPassword"
                                class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full"
                                type="password" id="confirmPassword" required placeholder="Confirma tu contraseña" @blur="checkConfirmPass">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="confirmPassword === ''">
                                    <i v-show="showMessageCP" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageCP" :fieldValue="confirmPassword"
                            errorMessage="Por favor confirma tu contraseña" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="phoneNumber">Número de telefono:</label>
                        <div class="flex items-baseline">
                            <input v-model.number="phoneNumber"
                                class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full"
                                type="tel" id="phoneNumber" required placeholder="Escribe tu número de telefono"
                                pattern="[0-9]{10}" @blur="checkPhoneNumber">
                            
                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="phoneNumber === ''">
                                    <i v-show="showMessagePN" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessagePN" :fieldValue="phoneNumber"
                            errorMessage="Por favor ingresa tu número de telefono" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label class="form-label" for="movileNumber">Numero de celular:</label>
                        <div class="flex items-baseline">
                            <input v-model="movileNumber"
                                class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full"
                                type="tel" id="movileNumber" required placeholder="Escribe tu número de celular" pattern="[0-9]{10}"
                                minlength="10" maxlength="10" @blur="checkMovileNumber">
                            
                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="movileNumber === ''">
                                    <i v-show="showMessageMV" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageMV" :fieldValue="movileNumber"
                            errorMessage="Por favor ingresa tu número celular" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                </div>
            </form>
            <!-- Buttons section -->
            <div class="flex justify-around py-16">
                <button class="m-0 bg-stone-800 rounded-lg text-white px-6" @click="goToSection(1)">Anterior</button>
                <button class="m-0  bg-stone-800 rounded-lg text-white px-6" @click="goToSection(3)">Siguiente</button>
            </div>

        </div>

        <!-- Section -->
        <div v-if="section === 3" class="w-11/12 bg-slate-300 rounded-lg flex flex-col h-full">

            <form @submit.prevent="contact">
                <!-- Row container -->
                <div class="flex flex-row justify-evenly py-2.5 flex-wrap">

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label for="address">Dirección:</label>
                        <div class="flex items-baseline">
                            <input v-model="address"
                                class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full"
                                type="text" id="address" required placeholder="Ingresa tu dirección" @blur="checkAddres">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="address === ''">
                                    <i v-show="showMessageAD" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessageAD" :fieldValue="address"
                            errorMessage="Por favor ingresa tu dirección" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>

                    <!-- Field -->
                    <div class="py-2.5 flex flex-col w-80">
                        <label for="postalCode">Código postal:</label>
                        <div class="flex items-baseline">
                            <input type="text" id="postalCode"
                                class="text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" required
                                v-model="postalCode" placeholder="Ingresa tu código postal" @blur="checkPostalCode">

                            <!-- Verify icon -->
                            <div class="text-sm ps-1.5 ">
                                <template v-if="postalCode === ''">
                                    <i v-show="showMessagePC" class="fas fa-times text-red-500"></i>
                                </template>
                                <template v-else>
                                    <i class="fas fa-check text-green-500"></i>
                                </template>
                            </div>
                        </div>

                        <!-- Verify field and show text-->
                        <FieldMessage :showMessage="showMessagePC" :fieldValue="postalCode"
                            errorMessage="Por favor selecciona tu código postal" successMessage="¡Genial!">
                        </FieldMessage>
                    </div>
                </div>
            </form>
            <!-- Sections Buttons -->
            <div class="flex justify-around py-16">
                <button class="m-0 bg-stone-800 rounded-lg text-white px-6" @click="goToSection(2)">Anterior</button>
                <button type="submit" class="m-0 bg-stone-800 rounded-lg text-white px-6"
                    @click="submitForm">Enviar</button>
            </div>
        </div>
    </div>
</template>

<script>

import axios from 'axios';
import 'flatpickr/dist/flatpickr.css';
import FlatPickr from 'vue-flatpickr-component';
//import moment from 'moment';
import FieldMessage from './verifyComponents/FieldMessage.vue';
import LinkCssAwm from './resources/LinkCssFontAwesome.vue';


export default {
    name: 'FormStruct',

    components: {
        FlatPickr,
        FieldMessage,
        LinkCssAwm
    },

    data() {
        return {
            section: 1,
            country: '',
            selectedCountry: '',
            showMessageC: false,
            gender: '',
            selectedGender: '',
            showMessageG: false,
            touched: false,
            errorMessage: '',
            name: '',
            selectedName: '',
            showMessageN: false,
            lastname: '',
            selectedLastname: '',
            showMessageL: false,
            idNumber: '',
            selectedIdNumber: '',
            showMessageID: false,
            isValidIdNumber: false,
            imageFront: '',
            showMessageIF: false,
            isFileSelected: false,
            imageBack: '',
            showMessageIB: false,
            email: '',
            showMessageEM: false,
            password: '',
            showMessagePS: false,
            confirmPassword: '',
            showMessageCP: false,
            phoneNumber: '',
            showMessagePN: false,
            movileNumber: '',
            showMessageMV: false,
            address: '',
            showMessageAD: false,
            postalCode: '',
            showMessagePC: false,

            date: '',
            options: {
                dateFormat: 'd/m/Y',
                maxDate: 'today'
            },
            showMessage: false,
            isValidDate: false,


            formData: {
                section1: {
                    country: '',
                    gender: '',
                    name: '',
                    lastname: '',
                    birthday: '',
                    idNumber: '',
                    imageFront: '',
                    imageBack: '',
                },
                section2: {
                    field3: '',
                    field4: '',
                    // ...
                },
                // ...
            },



        };
    },
    methods: {

        // Method that allow check the field and control the text
        checkCountry() {
            if (this.country === '') {
                this.showMessageC = true;
                this.formIsValid = false;
            } else {
                this.showMessageC = false;
                this.selectedCountry = this.country;
                this.formIsValid = true;
            }
        },

        // Method that allow check the field and control the text
        checkGender() {
            if (this.gender === '') {
                this.showMessageG = true;
            } else {
                this.showMessageG = false;
                this.selectedGender = this.gender;
            }
        },

        // Method that allow check the field and control the text
        checkName() {
            if (this.name === '') {
                this.showMessageN = true;
            } else {
                this.showMessageN = false;
            }
        },

        // Method that allow check the field and control the text
        checkLastname() {
            if (this.lastname === '') {
                this.showMessageL = true;
            } else {
                this.showMessageL = false;
            }
        },

        // Method that allow validate the age and show a message
        checkAge() {
            const birthdate = new Date(this.date);
            const now = new Date();
            let age = now.getFullYear() - birthdate.getFullYear();
            const monthDiff = now.getMonth() - birthdate.getMonth();
            if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < birthdate.getDate())) {
                age--;
            }
            this.isValidDate = age >= 18;
            this.showMessage = true;
        },

        // Method that allow check the field and control the text
        checkIdNumber() {
            if (this.idNumber === '') {
                this.showMessageID = true;
            } else {
                this.showMessageID = false;
            }
        },

        // Method that allow check the field and control the text
        checkImageFront() {
            if (this.imageFront === '') {
                this.showMessageIF = true;
            } else {
                this.showMessageIF = false;
            }
        },

        // Method that allow check the field and control the text
        checkImageBack() {
            if (this.imageBack === '') {
                this.showMessageIB = true;
            } else {
                this.showMessageIB = false;
            }
        },

        // Method that allow charger a file 
        onFileSelect(event) {
            const file = event.target.files[0];
            if (file && file.type === 'image/jpeg') {
                this.imageFront = file;
                this.showMessageIF = false;
            } else {
                this.showMessageIF = true;
            }
        },

        onFileSelect2(event) {
            const file = event.target.files[0];
            if (file && file.type === 'image/jpeg') {
                this.imageBack = file;
                this.showMessageIB = false;
            } else {
                this.showMessageIB = true;
            }
        },

        // Method that allow check the field and control the text
        checkEmail() {
            if (this.email === '') {
                this.showMessageEM = true;
            } else {
                this.showMessageEM = false;
            }
        },

        // Method that allow check the field and control the text
        checkPassword() {
            if (this.password === '') {
                this.showMessagePS = true;
            } else {
                this.showMessagePS = false;
            }
        },

        // Method that allow check the field and control the text
        checkConfirmPass() {
            if (this.confirmPassword === '') {
                this.showMessageCP = true;
            } else {
                this.showMessageCP = false;
            }
        },

        // Method that allow check the field and control the text
        checkPhoneNumber() {
            if (this.phoneNumber === '') {
                this.showMessagePN = true;
            } else {
                this.showMessagePN = false;
            }
        },

        // Method that allow check the field and control the text
        checkMovileNumber() {
            if (this.movileNumber === '') {
                this.showMessageMV = true;
            } else {
                this.showMessageMV = false;
            }
        },

        // Method that allow check the field and control the text
        checkAddres() {
            if (this.address === '') {
                this.showMessageAD = true;
            } else {
                this.showMessageAD = false;
            }
        },

        // Method that allow check the field and control the text
        checkPostalCode() {
            if (this.postalCode === '') {
                this.showMessagePC = true;
            } else {
                this.showMessagePC = false;
            }
        },


        // Method to check data fields and display them in console
        submitForm() {
            if (this.country === "") {
                console.log('Faltan los datos de country')
                return;
            }
            if (this.gender === "") {
                console.log('Faltan los datos de gender')
                return;
            }
            if (this.name === "") {
                console.log('Faltan los datos de name')
                return;
            }
            if (this.lastname === "") {
                console.log('Faltan los datos de lastname')
                return;
            }
            if (this.birthday === "") {
                console.log('Faltan los datos de birthday')
                return;
            }
            if (this.idNumber === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.imageFront === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.imageBack === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.email === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.password === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.confirmPassword === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.phoneNumber === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.movileNumber === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.address === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }
            if (this.postalCode === "") {
                console.log('Faltan los datos de idNumber')
                return;
            }

            /*if (this.password !== this.confirmPassword) {
                // mostrar un mensaje de error
                console.log('Las contraseñas no coinciden')
                return
            }*/

            // Show in console
            console.log('Formulario enviado',
                {
                    country: this.country,
                    gender: this.gender,
                    name: this.name,
                    lastname: this.lastname,
                    birthday: this.birthday,
                    idNumber: this.idNumber,
                    imageFront: this.imageFront,
                    imageBack: this.imageBack,
                    email: this.email,
                    password: this.password,
                    confirmPassword: this.confirmPassword,
                    phoneNumber: this.phoneNumber,
                    movileNumber: this.movileNumber,
                    address: this.address,
                    postalCode: this.postalCode
                }
            )
        },


        // Method that give the life to the buttoms
        /*goToSection(section) {
            // Validar los campos de la sección actual
            const fields = Object.values(this.formData['section' + section]);
            const areAllFieldsFilled = fields.every((value) => value !== '');

            if (!areAllFieldsFilled) {
                // Si no están todos llenos, mostrar un mensaje de error y no avanzar
                alert('Por favor, llene todos los campos antes de continuar.');
                return;
            }

            // Si todos los campos están llenos, avanzar a la siguiente sección
            this.currentSection = section;
        },*/



        goToSection(sectionNumber) {
            this.section = sectionNumber;
        },



    },

    // Allow control the message in each field
    watch: {

        country(newVal) {
            this.touched = newVal === '';
        },

        gender(newValg) {
            this.touched = newValg === '';
        },

        name(newValN) {
            this.touched = newValN === '';
        },

        lastname(newValL) {
            this.touched = newValL === '';
        },

        birthday(newValB) {
            this.touched = newValB === '';
        },

        idNumber(newValID) {
            this.touched = newValID === '';
        },

        imageFront(newValIF) {
            this.touched = newValIF === '';
        },

        imageBack(newValIB) {
            this.touched = newValIB === '';
        },

        email() {
            this.checkValidity();
        },
    },

    // Function that allow get all list country altrough API
    created() {
        axios.get('https://restcountries.com/v2/all')
            .then(response => {
                this.countries = response.data;
            })
            .catch(error => {
                console.log(error);
            });
    },

    // This allows you to control the number of countries displayed on the screen 
    computed: {
        limitedCountries() {
            return this.countries.slice(0, 5);
        }
    }
}
</script>
