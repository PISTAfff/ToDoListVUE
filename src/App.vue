<template>
  <div>
    <div class="MainContainer">
      <h1 class="Title">To Do List</h1>
      <p class="AddANote">Add a note!</p>
      <div class="InputContainer">
        <input
          class="InputArea"
          v-model="userInput"
          placeholder="eg: Feed My Cat!"
          @input="handleChange"
        />
      </div>
      <div class="ButtonContainer">
        <button class="Button" @click="addNote">Add Note</button>
      </div>
      <hr />
      <div class="NoteContainer">
        <NoteComponents
          v-for="(note, index) in notes"
          :key="index"
          :Note="note"
          :CheckState="check[index]"
          @delete="removeNote(index)"
          @edit="editNote(index)"
          @check="checkNote(index)"
        />
      </div>
    </div>
    <div class="BlackBackground" v-if="EditComponent">
      <div class="Container">
        <h1 class="Title">Edit Note</h1>

        <div class="InputContainer">
          <input
            class="InputArea"
            v-model="newedit"
            :placeholder="[this.notes[this.keys.indexOf(this.editing)]]"
          />
        </div>
        <div class="ButtonsContainer">
          <div class="ButtonContainer">
            <button class="Button Red" @click="cancel">Cancel</button>
          </div>
          <div class="ButtonContainer">
            <button class="Button" @click="finishEdit">Edit Note</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NoteComponents from "./components/NoteComponents.vue";

export default {
  name: "App",
  components: { NoteComponents },
  data() {
    return {
      userInput: "",
      notes: [],
      check: [],
      keys: [],
      counter: 0,
      editing: "",
      newedit: "",
      EditComponent: false,
    };
  },
  methods: {
    handleChange() {
      if (this.userInput.length > 25) {
        this.userInput = this.userInput.substring(0, 25);
      }
    },
    addNote() {
      if (this.userInput.trim() !== "") {
        this.keys.push(this.counter);
        this.notes.push(this.userInput);
        this.check.push(false);
        this.userInput = "";
        this.counter++;
      }
    },
    removeNote(index) {
      this.notes.splice(index, 1);
      this.check.splice(index, 1);
      this.keys.push(index, 1);
    },
    editNote(index) {
      this.EditComponent = true;
      this.editing = this.keys[index];
    },
    finishEdit() {
      this.notes[this.keys.indexOf(this.editing)] = this.newedit;
      this.EditComponent = false;
      this.editing = "";
      this.newedit = "";
    },
    cancel() {
      this.EditComponent = false;
      this.editing = "";
      this.newedit = "";
    },
    checkNote(index) {
      this.check[index] = !this.check[index];
    },
  },
};
</script>
<style>
html,
body,
#app {
  height: 100%;
  margin: 0;
}
#app {
  display: flex;
  justify-content: center;
  align-content: center;
  background-color: #e8eef2;
  align-items: center;
  font-family: monospace;
}
hr {
  width: 75%;
}
.MainContainer {
  scale: 1.5;
  display: flex;
  justify-content: start;
  align-content: center;
  flex-direction: column;
  background-color: #f9fdff;
  width: 250px;
  height: 400px;
  border-radius: 5px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px,
    rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
  user-select: none;
}
.Title {
  justify-content: center;
  align-content: center;
  text-align: center;
  width: 100%;
  font-size: 22px;
  height: 10%;
  margin: 0%;
  margin-top: 20px;
}

.AddANote {
  justify-content: center;
  align-content: center;
  text-align: center;
  width: 100%;
  height: 5%;
  font-size: 12px;
  margin: 0%;
}
.InputContainer,
.ButtonContainer {
  display: flex;
  justify-content: center;
  align-content: center;
  width: 100%;
  height: 10%;
  margin-top: 15px;
}
.InputArea {
  width: 90%;
  height: 25px;
  font-size: 12px;
  margin: 0;
  padding: 0;
  border: none;
  box-shadow: rgba(0, 0, 0, 0.02) 0px 1px 3px 0px,
    rgba(27, 31, 35, 0.15) 0px 0px 0px 1px;
  border-radius: 2px;
  padding-left: 5px;
  background-color: #e8eef2;
  outline: none;
}
.ButtonContainer {
  margin-top: 0px;
}
.Button {
  transition: 0.25s;
  width: 50%;
  height: 25px;
  font-size: 12px;
  margin: 0;
  padding: 0;
  border: none;
  box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px;
  border-radius: 2px;
  background-color: #e8eef2;
  outline: none;
}
.Button:hover {
  transition: 0.55s;
  width: 55%;
  background-color: #1b065e;
  color: white;
  cursor: pointer;
}
.NoteContainer {
  width: 100%;
  height: 50%;
  padding: 20px 0;
  overflow-y: scroll;
}
.BlackBackground {
  position: absolute;
  top: 0%;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: rgba(0, 0, 0, 0.451);
  width: 100%;
  height: 100%;
}
.Container {
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: #e8eef2;
  gap: 25px;
  width: 250px;
  height: 25%;
}
.ButtonsContainer {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: start;
  height: 30%;
}
</style>
