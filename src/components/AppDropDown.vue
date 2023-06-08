<script setup lang="ts">
import type { DropDownOption, DropDown } from '@/types';
import { computed } from 'vue';

const props = defineProps<{
    options: Array<DropDownOption[]>,
    id: string,
    modelValue: DropDownOption,
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
    set(value: DropDownOption){
        if(value){
            emit('update:modelValue', { id: props.id, value })
        }
    }
})

const handleRemove = () => {
    emit('delete', { id: props.id, value: props.modelValue } as DropDown)
}
</script>

<template>
  <div class="app-drop-down d-flex align-center">
    <v-icon class="app-drop-down__draggable mr-4" size="large">mdi-drag</v-icon>
    <v-autocomplete
        :items="options"
        item-value="key"
        item-title="value"
        variant="outlined"
        v-model="model"
        hide-details
        persistent-hint
        return-object
        class="w-full"
    ></v-autocomplete>
    <v-btn
        variant="plain"
        class="px-0"
        density="compact"
        :disabled="disableDelete"
        @click="handleRemove"
    >
        <v-icon color="red">mdi-close</v-icon>
    </v-btn>
  </div>
</template>

<style scoped>
.app-drop-down__draggable {
    cursor: grab;
    visibility: hidden;
    pointer-events: none;
}
.app-drop-down:hover .app-drop-down__draggable {
    visibility: visible;
    pointer-events: all;
}
</style>
