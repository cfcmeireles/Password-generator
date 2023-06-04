<template>
  <div>
    <p>What length would you like your new password to have?</p>
    <select v-model="password.length">
      <option disabled selected value>-- select an option --</option>
      <option>8</option>
      <option>12</option>
      <option>16</option>
    </select>
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
    <div>New password is: {{ password.newPassword.join("") }}</div>
    <button @click="generatePassword">
      Click here to generate a new password
    </button>
  </div>
</template>
  
  <script>
export default {
  data() {
    return {
      password: {
        // timesEachCharacter: [],
        length: [],
        newPassword: [],
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
      this.password.newPassword = [];
      let passwordRequirements = [this.selectedRequirements];
      for (var i = 0; i < this.password.length; i++) {
        passwordRequirements.forEach((req) => {
          const randomValue = Math.floor(Math.random() * req.length);
          const result = req[randomValue];
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