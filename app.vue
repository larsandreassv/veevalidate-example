<template>
  <div class="flex flex-col w-96 gap-4 p-2 bg-stone-50 border rounded-sm m-2">
    <div class="flex flex-col p-2 border rounded-sm">
      <FormInput v-model="values.foo" label="foo" name="foo" required />
      <FormInput v-model="bar" name="bar" label="bar" required />
    </div>

    <div class="flex flex-col p-2 border rounded-sm">
      <span>foo: {{ values.foo }}</span>
      <span>bar: {{ bar }}</span>
    </div>

    <button :disabled="meta.pending" @click="save">Save</button>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { useForm } from "vee-validate";

const bar = ref("bar");

const { values, handleSubmit, meta } = useForm({
  initialValues: {
    foo: "foo",
  },
});

const save = handleSubmit((values) => {
  console.log("saving");
  console.log(values);
});
</script>
