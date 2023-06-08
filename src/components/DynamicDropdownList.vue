<script setup lang="ts">
import AppDropDown from '@/components/AppDropDown';
import { computed, ref } from 'vue';
import type { DropDown, DropDownOption } from '@/types';
import draggable from "vuedraggable";

const MINIMUM_VALUE = 3;
const MAXIMUM_VALUE = 8;

const props = defineProps<{
    options: DropDownOption[]
}>()

const generateRandomId = () => crypto.randomUUID()

const initDefaultSelection = <T>(
  callback: (_: undefined, idx: number) => T
): T[] => {
  return Array(5)
    .fill(undefined)
    .map(callback);
};

const selectedOptions = ref<string[]>(initDefaultSelection((_: undefined, idx: number): string => props.options[idx].key))

const dropdowns = ref(initDefaultSelection((_: undefined, idx: number): DropDown  => ({
  value: props.options[idx], 
  id: generateRandomId(),
})))

const dragOptions = ref({
  animation: 200,
  handle: ".app-drop-down__draggable",
  itemKey: 'option'
})

const filteredOptions = computed((): DropDownOption[] => {
  return props.options.filter(option => !selectedOptions.value.includes(option.key))
})

const isDeleteDisabled = computed((): boolean => {
  return dropdowns.value.length <= MINIMUM_VALUE
})

const isAddDisabled = computed((): boolean => {
  return dropdowns.value.length >= MAXIMUM_VALUE
})

const handleValueChange = (dropdown: DropDown) => {
  const currentDropDown = dropdowns.value.find(({ id }) => dropdown.id === id)

  if(currentDropDown){
    removeSelectedKey(currentDropDown.value.key)
    selectedOptions.value.push(dropdown.value.key)
    currentDropDown.value = dropdown.value
  }
}

const handleRemove = (dropdown: DropDown) => {
  removeSelectedKey(dropdown.value.key)
  dropdowns.value = dropdowns.value.filter(({ id }) => id !== dropdown.id)
}

const removeSelectedKey = (removedKey: string) => {
  selectedOptions.value = selectedOptions.value.filter(key => key !== removedKey)
}

const handleAdd = () => {
  dropdowns.value.push({
  value: { value: '', key: '' } as DropDownOption, 
  id: generateRandomId(),
})
}
</script>

<template>
  <v-container class="pa-8">
    <v-card width="600" class="mx-auto pa-8">
      <h2 class="text-center mb-8">Drop down vue app</h2>
      <draggable
        v-model="dropdowns"
        v-bind="dragOptions"
      >
        <template #item="{ element }">
          <AppDropDown 
            :id="element.id"  
            :model-value="element.value"
            :disable-delete="isDeleteDisabled"
            @update:modelValue="handleValueChange"
            @delete="handleRemove"
            :options="filteredOptions"
            class="mb-4"
          />
        </template>
      </draggable>
      
      <v-btn @click="handleAdd" :disabled="isAddDisabled" prepend-icon="mdi-plus" variant="tonal">
        Add
      </v-btn>
    </v-card>
  </v-container>
</template>
