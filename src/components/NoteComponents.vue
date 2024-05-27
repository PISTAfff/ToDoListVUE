<template>
  <div class="NoteMainContainer">
    <div class="NoteSubContainer">
      <input
        id="CheckBox"
        type="checkbox"
        class="CheckBox"
        v-model="isChecked"
        @click="Check"
      />
      <p :class="['Note', this.CheckState ? 'checked' : '']">
        {{ this.Note }}
      </p>
    </div>
    <div class="NoteSubContainer">
      <button class="EditBtn Btn" @click="Edit">Edit</button>
      <button class="DeleteBtn Btn" @click="Delete">Delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoteComponents",
  props: {
    Note: {
      type: String,
      required: true,
    },
    CheckState: {
      type: Boolean,
      required: true,
    },
  },

  data() {
    return {
      isChecked: this.CheckState,
    };
  },
  watch: {
    CheckState: {
      handler() {
        this.isChecked = this.CheckState;
      },
      deep: true,
    },
  },
  methods: {
    Delete() {
      this.$emit("delete");
    },
    Edit() {
      this.$emit("edit");
    },
    Check() {
      this.$emit("check");
    },
  },
};
</script>
<style>
.NoteMainContainer {
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: start;
  align-content: center;
  flex-direction: column;
}

.NoteSubContainer {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 100%;
  height: 35%;
}
.Note {
  display: flex;
  align-content: center;
  width: 155px;
  height: fit-content;
  font-size: 12px;
  margin: 0%;
}
.CheckBox {
  margin-right: 12.5px;
}
.CheckBox:hover {
  cursor: pointer;
}
.Note.checked {
  text-decoration: line-through;
}
.Btn {
  transition: 0.25s;
  border: none;
  font-size: 12px;
  width: fit-content;
  padding: 3px 25px;
  margin: 0 10px;
  border-radius: 2px;
  box-shadow: rgba(255, 255, 255, 0.2) 0px 0px 0px 1px inset,
    rgba(0, 0, 0, 0.9) 0px 0px 0px 1px;
}
.DeleteBtn {
  background-color: #d05353;
  color: #e8eef2;
}
.Btn:hover {
  transition: 0.25s;
  padding: 3px 27.5px;
  cursor: pointer;
}
</style>
