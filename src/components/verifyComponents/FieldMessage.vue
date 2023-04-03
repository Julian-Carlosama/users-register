<template>
    <div class="text-sm">
        <span v-show="showMessage && fieldValue === ''" class="text-red-500">{{ errorMessage }}</span>
        <span v-show="fieldValue !== ''" class="text-green-500">{{ successMessage }}</span>
    </div>
</template>
  
<script>
export default {
    name: 'FieldMessage',
    props: {
        showMessage: {
            type: Boolean,
            //default: false
            required: true
        },
        fieldValue: {
            type: String,
            //default: ''
            required: true
        },
        //Values that allow send after the form
        errorMessage: {
            type: String,
            default: 'Por favor llena este campo'
        },
        successMessage: {
            type: String,
            default: '¡Genial, has completado este campo!'
        }
    }
}
</script>
