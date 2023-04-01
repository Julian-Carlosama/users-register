<template>
    <section class="flex-shrink-0 w-screen h-full bg-slate-400">
        <form action class="form" @submit.prevent="submitForm">
            <label for="country">Pais:</label>
            <select v-model="selectedCountry" class="select max-h-40 border overflow-y-scroll" id="country" required>
                <option value="">Selecciona un país</option>
                <option v-for="(country, index) in countries" :key="index" :value="country.name">
                    {{ country.name }}
                </option>
            </select>

            <label class="form-label" for="#gender">Género:</label>
            <select v-model="gender" class="form-select" id="gender" required>
                <option value="">Selecciona tu género</option>
                <option value="Hombre">Hombre</option>
                <option value="Mujer">Mujer</option>
                <option value="Prefiero no especificar">Prefiero no especificar</option>
            </select>

            <label class="form-label" for="#name">Nombre:</label>
            <input v-model="name" class="form-input" type="text" id="name" required placeholder="Escribe tu nombre">

            <label class="form-label" for="idNumber">Identificación:</label>
            <input v-model.number="idNumber" class="form-input" type="number" id="idNumber" required
                placeholder="Escribe tu identificación">

            <label class="form-label" for="#imageBack">Foto documento reverso:</label>
            <input v-on:change="onFileSelect" class="form-input" type="file" id="image" required
                placeholder="Imagen reverso en formato jpg">

            <button class="ml-auto" @click="goToNextSection">Siguiente</button>
        </form>
    </section>
</template>
  
<script>
import axios from 'axios';

export default {
    name: 'CountrySelection',
    data() {
        return {
            steps: ['Paso 1', 'Paso 2', 'Paso 3'],
            currentStep: 1,
            selectedCountry: '',
            countries: [],
            gender: '',
            name: '',
            idNumber: '',
            imageUrl: '',
        };
    },
    methods: {
        submitForm() {
            if (this.password !== this.confirmPassword) {
                // mostrar un mensaje de error
                console.log('Las contraseñas no coinciden')
                return
            }
            // enviar el formulario
            console.log('Formulario enviado')
        },
    },
    created() {
        axios.get('https://restcountries.com/v2/all')
            .then(response => {
                this.countries = response.data;
            })
            .catch(error => {
                console.log(error);
            });
    },
}
