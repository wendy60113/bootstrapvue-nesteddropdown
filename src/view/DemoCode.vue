<template>
  <NestedDropdown
    v-model="modelData"
    :option="optionList"
  />
</template>

<script>
export default {
  data:()=>({
    modelData:'',
    optionList:[
      {
        title: "First Title",
        content: ["First Action", "Second Action"],
      },
      {
        title: "Second Title",
        content: ["First Content", "Second Content", "Third Content"],
      },
    ]
  })
}
</script>