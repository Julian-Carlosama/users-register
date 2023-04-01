<template>
    <!-- Strucuture Form container -->
    <div class="flex flex-col h-4/5 overflow-x-hidden">

        <!-- Container 1 -->
        <section class="h-4/5 overflow-hidden w-full text-xl ">

            <!-- Form Container  -->
            <div class="w-full bg-slate-300 h-full rounded-lg">
                <form action class="" @submit.prevent="contact">

                    <!-- Container row country and gender -->
                    <div class="flex-grow flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label for="country">Pais:</label>
                            <select v-model="selectedCountry" 
                                class="select text-base h-8 text-slate-400 border overflow-y-scroll rounded-md max-w-4xl w-2/5 min-w-full" id="country" required
                                @change="checkFields"
                                >
                                <option value="" >Selecciona un país</option>
                                <option  v-for="(country, index) in countries" :key="index" :value="country.name">
                                    {{ country.name }}</option>
                            </select>
                            <div
                                v-bind:class="{ 'text-green-500': fieldValues.country, 'text-red-500': !fieldValues.country }">
                                <i v-if="fieldValues.country" class="fas fa-check"></i>
                                <i v-else class="fas fa-times"></i>
                            </div>
                        </div>
                        <div class="py-2.5 flex flex-col  w-80">
                            <label class="form-label" for="gender">Género:</label>
                            <select v-model="gender" class="text-base h-8 text-slate-400 form-select rounded-md max-w-7xl w-3/6 min-w-full" id="gender" required>
                                <option value="">Selecciona tu género</option>
                                <option value="Hombre">Hombre</option>
                                <option value="Mujer">Mujer</option>
                                <option value="Prefiero no especificar">Prefiero no especificar</option>
                            </select>
                        </div>
                    </div>

                    <!-- Container row Name Lastname -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="name">Nombre:</label>
                            <input v-model="name" class="text-base h-8 text-slate-400 form-input rounded-md max-w-7xl w-3/6 min-w-full" type="text" id="name" required
                                placeholder="Escribe tu nombre">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="lastName">Apellido:</label>
                            <input v-model="string" class="text-base h-8 text-slate-400 form-input rounded-md max-w-7xl w-3/6 min-w-full" type="text" id="lastName" required
                                placeholder="Escribe tu apellido">
                        </div>
                    </div>


                    <!-- Container row country birthday idNumber -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="birthday">Fecha de Nacimiento:</label>
                            <!--input v-model="date" class="form-input rounded-md" type="text" id="name" required
                                placeholder="day/mon/yea"-->
                            <flat-pickr class="text-base h-8 text-slate-400 form-select rounded-md max-w-7xl w-3/6 min-w-full" v-model="date" id="birthday" :options="options" />
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="idNumber">Identificación:</label>
                            <input v-model.number="idNumber" class="text-base h-8 text-slate-400 form-input rounded-md max-w-7xl w-3/6 min-w-full" type="number" id="idNumber"
                                required placeholder="Escribe tu identificación">
                        </div>
                    </div>

                    <!-- Container row Documnet file -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="imageFront">Foto documento frontal:</label>
                            <input v-on:change="onFileSelect" class="form-input" type="file" id="image" required
                                placeholder="Imagen frontal en formato jpg">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="imageBack">Foto documento reverso:</label>
                            <input v-on:change="onFileSelect" class="form-input" type="file" id="image" required
                                placeholder="Imagen reverso en formato jpg">
                        </div>
                    </div>
                </form>

                <!-- Buttons section -->
                <div class="flex justify-center py-16">
                    <button class="m-0  bg-stone-800 rounded-lg text-white px-6" @click="goToSection(2)">Siguiente</button>
                </div>
            </div>
        </section>


        <!-- Container 2 -->
        <section class="hidden h-4/5 w-full text-xl">

            <!-- Form Container -->
            <div class="w-full bg-slate-300 h-full rounded-lg">
                <form action class="form" @submit.prevent="contact">

                    <!-- Container row email and password -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label for="email">Email:</label>
                            <input v-model="email" class="form-input text-base h-8 text-slate-400  rounded-md max-w-7xl w-3/6 min-w-full" type="email" id="email" reuired
                                placeholder="Escribe tu email">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="Password">Contraseña:</label>
                            <input v-model="password" class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" type="password" id="password" required
                                placeholder="Escribe tu contraseña">
                        </div>
                    </div>


                    <!-- Container row confirm password, phonenumber movilNumber -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="confirmPassword">Confirmar contraseña:</label>
                            <input v-model="confirmPassword" class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" type="password" id="confirmPassword" required
                                placeholder="Confirma tu contraseña">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="phoneNumber">Número de telefono:</label>
                            <input v-model.number="phoneNumber" class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" type="tel" id="phoneNumber" required
                                placeholder="Escribe tu número de telefono" pattern="[0-9]{10}">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label class="form-label" for="movileNumber">Numero de celular:</label>
                            <input v-model="movileNumber" class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" type="tel" id="name" required
                                placeholder="Escribe tu número de celular" pattern="[0-9]{10}" minlength="10" maxlength="10">
                        </div>
                    </div>
                </form>
                <!-- Buttons section -->
                <div class="flex justify-around py-16">
                    <button class="m-0 bg-stone-800 rounded-lg text-white px-6" @click="goToSection(1)">Anterior</button>
                    <button class="m-0  bg-stone-800 rounded-lg text-white px-6" @click="goToSection(3)">Siguiente</button>
                </div>
            </div>

            
        </section>

        <!-- Container 3 -->
        <section class="hidden h-4/5 w-full text-xl ">

            <!-- Form Container  -->
            <div class="w-full bg-slate-300 h-full rounded-lg ">
                <form action class="form" @submit.prevent="contact">

                    <!-- Container row country and gender -->
                    <div class="flex flex-row justify-evenly py-2.5 flex-wrap">
                        <div class="py-2.5 flex flex-col w-80">
                            <label for="address">Dirección:</label>
                            <input v-model="address" class="form-input text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" type="text" id="address" required placeholder="Ingresa tu dirección">
                        </div>
                        <div class="py-2.5 flex flex-col w-80">
                            <label for="postalCode">Código postal:</label>
                            <input type="text" id="postalCode" class="text-base h-8 text-slate-400 rounded-md max-w-7xl w-3/6 min-w-full" required v-model="postalCode" placeholder="Ingresa tu código postal">
                        </div>
                    </div>    
                </form>
                
                <!-- Button send -->
                <div>
                    
                </div>
                <!-- Sections Buttons -->
                <div class="flex justify-around py-16">
                    <button class="m-0 bg-stone-800 rounded-lg text-white px-6" @click="goToSection(2)">Anterior</button>
                    <button class="m-0 bg-stone-800 rounded-lg text-white px-6" @click="goToSection(2)">Enviar</button>
                    
                </div>
                 
            </div>
            
           
        </section>
    </div>
</template>

<script>
import axios from 'axios';
import 'flatpickr/dist/flatpickr.css';
import FlatPickr from 'vue-flatpickr-component';
import moment from 'moment';


//import LineLife from './LineLife.vue'


export default {

    // eslint-disable-next-line vue/multi-word-component-names
    name: 'FormStructure',

    components: {
        FlatPickr,
        //LineLife
    },

    methods: {

        // Funcrion that allow check full fields
        checkFields() {
            const requiredFields = [
                "country", 
                "gender", 
                "name", 
                "lastName", 
                "date", 
                "idNumber", 
                "frontImage", 
                "backImage"
        ];
            requiredFields.forEach(field => {
                const value = this[field];
                this.fieldValues[field] = value;
            });
        },


        // Funcrion that allow check email field
        checkValidity() {
            if (this.name && this.email) {
                this.valid = true;
            } else {
                this.valid = false;
            }
        },

        watch: {
            name() {
                this.checkValidity();
            },
            email() {
                this.checkValidity();
            },
        },


        // Function that allow validate the age
        validateForm() {
            const selectedDate = moment(this.date, 'DD/MM/YYYY');
            const currentDate = moment();
            const age = currentDate.diff(selectedDate, 'years');

            if (age < 18) {
                // Mostrar un mensaje de error o hacer algo más
                console.log('mensaje de error');
                return false;
            }
            if (!this.selectedCountry) {
                // Mostrar un mensaje de error o hacer algo más
                console.log('Debes seleccionar un país');
                return false;
            }

            // Si la fecha es válida, enviar el formulario
            console.log('fecha es válida');
            return true;
        },

        // Funcrion that allow check passwords fields
        submitForm() {
            if (this.password !== this.confirmPassword) {
                // mostrar un mensaje de error
                console.log('Las contraseñas no coinciden')
                return
            }
            // enviar el formulario
            console.log('Formulario enviado')
        },


        // Funcrion that give the life to the buttoms
        goToSection(section) {
            const sections = document.querySelectorAll("section");
            sections.forEach((section) => section.classList.add('hidden'))
            sections[section - 1].classList.remove('hidden')
            sections[section - 1].scrollIntoView({
                behavior: "smooth"
            });
        },

        // Function that allow charger a file
        onFileSelected(event) {
            const file = event.target.files[0];
            const reader = new FileReader();
            reader.onload = event => {
                this.imageUrl = event.target.result;
            };
            reader.readAsDataURL(file);
        }
    },

    // This allow return the procesed values
    data() {
        return {
            selectedCountry: '',
            gender: '',
            name: '',
            lastName: '',
            date: '',
            idNumber: null,
            fontImage: null,
            backImage: null,
            fieldValues: {
                country: "",
                gender: "",
                name: "",
                lastName: "",
                date: "",
                idNumber: null,
                frontImage: null,
                backImage: null
            },

            //This is the new state
            steps1: ['Paso 1', 'Paso 2', 'Paso 3'],
            steps2: ['Etapa 1', 'Etapa 2', 'Etapa 3'],
            steps3: ['Fase 1', 'Fase 2', 'Fase 3'],
            currentStep1: 1,
            currentStep2: 1,
            currentStep3: 1,



            currentStep: 1,
            imageUrl: null,
            countries: [],


            password: '',
            confirmPassword: '',
            phoneNumber: '',
            postalCode: '',

            options: {
                dateFormat: 'd/m/Y',
            },
            valid: false
        };

    },


    // Fcution that allow get all list country altrough API
    created() {
        axios.get('https://restcountries.com/v2/all')
            .then(response => {
                this.countries = response.data;
            })
            .catch(error => {
                console.log(error);
            });
    },
    computed: {
        limitedCountries() {
            return this.countries.slice(0, 5);
        }
    }
};
</script>
