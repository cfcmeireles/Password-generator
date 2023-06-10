<template>
  <div>
    <p>What length would you like your new password to have?</p>

    <input v-model="password.length" type="range" min="8" max="16" step="4" />
    <output>{{ password.length }}</output>

    <div
      class="checkbox-items"
      v-for="requirement in requirements"
      :key="requirement.key"
    >
      <input
        type="checkbox"
        v-model="requirement.isChecked"
        @change="logSelectedRequirements"
      />
      {{ requirement.text }}
    </div>
    <div>
      New password is: {{ password.newPassword.join("") }}
      {{ password.newPassword.length }}
    </div>
    <button @click="generatePassword">
      Click here to generate a new password
    </button>
  </div>
  <p v-if="showAlert">Please check at least 1 requirement</p>
</template>
  
  <script>
export default {
  data() {
    return {
      password: {
        // timesEachCharacter: [],
        length: 12,
        newPassword: [],
        buttonClicked: false,
        showAlert: false,
      },
      requirements: [
        {
          key: 1,
          text: "Include Lower case letters",
          isChecked: false,
          characters: [
            "a",
            "b",
            "c",
            "d",
            "e",
            "f",
            "g",
            "h",
            "i",
            "j",
            "k",
            "l",
            "m",
            "n",
            "o",
            "p",
            "q",
            "r",
            "s",
            "t",
            "u",
            "v",
            "w",
            "x",
            "y",
            "z",
          ],
        },
        {
          key: 2,
          text: "Include Upper case letters",
          isChecked: false,
          characters: [
            "A",
            "B",
            "C",
            "D",
            "E",
            "F",
            "G",
            "H",
            "I",
            "J",
            "K",
            "L",
            "M",
            "N",
            "O",
            "P",
            "Q",
            "R",
            "S",
            "T",
            "U",
            "V",
            "W",
            "X",
            "Y",
            "Z",
          ],
        },
        {
          key: 3,
          text: "Include Numbers",
          isChecked: false,
          characters: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        },
        {
          key: 4,
          text: "Include Symbols",
          isChecked: false,
          characters: ["*", "@", "#", "$", "%", "&", "/", "?", "-", "+"],
        },
      ],
    };
  },
  computed: {
    selectedRequirements() {
      const filteredRequirements = this.requirements.filter(
        (requirement) => requirement.isChecked
      );
      const characters = filteredRequirements.flatMap(
        (requirement) => requirement.characters
      );
      return characters;
    },
    checkedRequirements() {
      const checkRequirements = this.requirements.filter(
        (checked) => checked.isChecked
      );
      return checkRequirements;
    },
  },
  methods: {
    logSelectedRequirements() {
      console.log("selectedRequirements:", this.selectedRequirements);
    },
    // generatePasswordLength() {
    //   this.password.newPassword = [];
    //   let passwordRequirements = [this.selectedRequirements];
    //   if (this.password.length == 8) {
    //     // this.password.passlength = 8;
    //     this.generatePassword(passwordRequirements);
    //   }
    //   if (this.password.length == 12) {
    //     this.password.passlength = 12;
    //     this.generatePassword(passwordRequirements);
    //   }
    //   if (this.password.length == 16) {
    //     this.password.passlength = 16;
    //     this.generatePassword(passwordRequirements);
    //   }
    // },
    generatePassword() {
      if (!this.checkedRequirements.length) {
        this.showAlert = true;
      } else {
        this.showAlert = false;
      }
      this.password.newPassword = [];
      let passwordRequirements = [this.selectedRequirements];
      for (var i = 0; i < this.password.length; i++) {
        passwordRequirements.forEach((req) => {
          const randomValue = Math.floor(Math.random() * req.length);
          const result = req[randomValue];
          console.log(result);
          this.password.newPassword.push(result);
        });
      }
    },
  },
};
</script>
  
<style scoped>
.checkbox-items {
  display: block;
}
</style>