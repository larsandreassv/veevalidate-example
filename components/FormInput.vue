<template>
    <div class="flex flex-col w-72">
        <label>{{ label }} {{ required ? '*' : '' }}</label>
        <input class="border" :value="value" @input="value = $event.target.value" />
        <span v-if="meta.touched" class="text-red-400">{{ errorMessage }}</span>
    </div>
</template>

<script lang="ts" setup>
import { computed } from 'vue'
import { useField } from 'vee-validate'
import { v4 as uuidv4 } from 'uuid'
import * as yup from 'yup'

interface Props {
    modelValue?: string
    label: string
    maxLength?: number
    required: boolean
    name: string
}

const props = defineProps<Props>();

const validationSchema = computed(() => {
    let schema = yup.string();
    if(props.maxLength) {
        schema = schema.max(props.maxLength, "Maks {{ max }} tegn");
    }
    if(props.required) {
        schema = schema.required("Påkrevd");
    }
    return schema;
})

//or random guid
const { value, errorMessage, meta } = useField(() => props.name ?? uuidv4(), validationSchema, {
    syncVModel: true,
    initialValue: props.modelValue,
});
</script>

