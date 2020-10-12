<template>
  <form class="edit-content" @submit.prevent="changeContent">
    <span class="header">Edit</span>
    <div
      class="edit"
      v-for="[index, content] in Object.entries(data.editContent)"
      :key="index"
    >
      <label class="header-two"
        ><strong>F{{ Number(index) + 1 }}{{ ": " }}</strong></label
      >
      <input
        type="text"
        class="editValue"
        :id="[editValue(index)]"
        :value="content"
        @change="changeValue($event, index)"
      /><br />
    </div>
    <button
      id="done"
      style="
        float: left;
        margin-top: 28px;
        border-radius: 4px;
        width: 75px;
        height: 30px;
        background-color: darkgrey;
      "
    >
      Done
    </button>
  </form>
</template>

<script>
import { onMounted, reactive } from "vue";
export default {
  name: "feed-edit",
  props: {
    contents: Object,
  },
  setup(props, attr) {
    const data = reactive({
      editContent: props.contents,
      editedContents: [],
    });

    const formatContents = onMounted(() => {
      data.editedContents = data.editContent.map((element, index) => {
        return { id: index, value: element };
      });
    });

    function editValue(index) {
      return "editValue " + index;
    }

    function changeValue(newval, index) {
      data.editedContents.find(
        (content) => content.id === Number(index)
      ).value = newval.srcElement.value;
    }

    function changeContent() {
      attr.emit("editedvalues", data.editedContents);
    }
    return { data, formatContents, editValue, changeValue, changeContent };
  },
};
</script>

<style>
.editValue {
  /* border-radius: 8px; */
  width: 220px;
  height: 18px;
  margin-top: 8px;
}

.header {
  font-style: bold;
  text-align: left;
  margin-top: 10%;
  font-size: 20px;
  font-family: Arial, Helvetica, sans-serif;
}

.header-two {
  font-size: 15px;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
