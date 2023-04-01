<template>
    <button @click="goToSection()">{{ buttonText }}</button>
</template>
  
<script>
    export default {
        props: {
            goToSection: {
                type: Function,
                required: true
            },
            currentSection: {
                type: Number,
                required: true
        }},
        methods: {
            goToNextSection() {
            this.goToSection(this.currentSection + 1);
            }
        }

    };
</script>
