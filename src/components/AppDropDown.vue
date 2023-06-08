<script setup lang="ts">
import type { DropDownOption, DropDown } from '@/types';
import { computed } from 'vue';

const props = defineProps<{
    options: Array<DropDownOption[]>,
    id: string,
    modelValue: string,
    disableDelete: boolean
}>()

const emit = defineEmits<{
    (event: 'delete', value: DropDown): void,
    (event: 'update:modelValue', value: DropDown): void,
}>()

const model = computed({
    get(){
        return props.modelValue
    },
    set(value: string){
        console.log(value);
        
        emit('update:modelValue', { id: props.id, value })
    }
})

const handleRemove = () => {
    emit('delete', { id: props.id, value: props.modelValue } as DropDown)
}
</script>

<template>
  <div class="d-flex align-items-center">
    <v-autocomplete
        :items="options"
        item-select="key"
        item-value="key"
        item-title="value"
        variant="outlined"
        v-model="model"
    ></v-autocomplete>
    <v-btn
        density="comfortable"
        variant="plain"
        :disabled="disableDelete"
        @click="handleRemove"
    >
        <template v-slot:append>
            <v-icon color="success">mdi-account</v-icon>
        </template>
    </v-btn>
  </div>
</template>

<style scoped>

</style>
