<template>
  <div id="password-generator">
    <div class="generated-password">{{ password.newPassword.join("") }}</div>
    <div class="main-div">
      <p>Character length</p>
      <output>{{ password.length }}</output>
      <input
        v-model="password.length"
        type="range"
        min="8"
        max="16"
        step="4"
        class="password-range"
      />

      <div
        class="checkbox-items"
        v-for="requirement in requirements"
        :key="requirement.key"
      >
        <input
          type="checkbox"
          v-model="requirement.isChecked"
          @change="passwordStrength"
        />
        {{ requirement.text }}
      </div>
      <div class="password-strength" @change="passwordStrength">
        {{ password.strength }}
      </div>
      <div class="strength-bars">
        <div
          class="bars"
          style="height: 24px; width: 2%"
          :style="`background-color: ${this.password.barColor1}`"
        ></div>
        <div
          class="bars"
          style="height: 24px; width: 2%"
          :style="`background-color: ${this.password.barColor2}`"
        ></div>
        <div
          class="bars"
          style="height: 24px; width: 2%"
          :style="`background-color: ${this.password.barColor3}`"
        ></div>
        <div
          class="bars"
          style="height: 24px; width: 2%"
          :style="`background-color: ${this.password.barColor4}`"
        ></div>
      </div>
      <button class="generate-btn" @click="generatePassword">Generate</button>
      <p v-if="showAlert">Please check at least 1 requirement</p>
    </div>
  </div>
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
        strength: "STRENGTH",
        barColor1: "",
        barColor2: "",
        barColor3: "",
        barColor4: "",
      },
      requirements: [
        {
          key: 1,
          text: "Include Lowercase Letters",
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
          text: "Include Uppercase Letters",
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
    passwordStrength() {
      if (this.checkedRequirements.length === 1) {
        this.password.strength = "WEAK";
        this.password.barColor1 = "#F3CD6C";
        this.password.barColor2 = "";
        this.password.barColor3 = "";
      } else if (
        this.checkedRequirements.length < 3 &&
        this.checkedRequirements.length > 1
      ) {
        this.password.strength = "MEDIUM";
        this.password.barColor2 = "#F3CD6C";
        this.password.barColor3 = "";
        this.password.barColor4 = "";
      } else if (
        this.checkedRequirements.length < 4 &&
        this.checkedRequirements.length > 1
      ) {
        this.password.strength = "MEDIUM";
        this.password.barColor3 = "#F3CD6C";
        this.password.barColor4 = "";
      } else if (this.checkedRequirements.length > 3) {
        this.password.strength = "STRONG";
        this.password.barColor4 = "#F3CD6C";
      } else {
        this.password.strength = "STRENGTH";
        this.password.barColor1 = "";
        this.password.barColor2 = "";
        this.password.barColor3 = "";
        this.password.barColor4 = "";
      }
    },
  },
};
</script>
  
<style>
#password-generator {
  /* display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 70px 500px; */
  width: 100%;
}

.generated-password {
  background: #24232b;
  height: 50px;
  /* grid-column-start: 2;
  grid-row-start: 1; */
  margin-bottom: 10px;
  display: flex;
  align-content: center;
  justify-content: center;
  align-items: center;
}

.main-div {
  background: #24232b;
  /* grid-column-start: 2;
  grid-row-start: 2; */
  height: 500px;
  width: 500px;
  padding: 20px;
}

.password-range {
  margin-bottom: 30px;
  width: 100%;
}
/* 
.password-range {
  background: red;
} */

/* .password-range::-moz-range-thumb {

  width: 25px;
  height: 25px;
  background: #04aa6d;
  cursor: pointer;
} */

.checkbox-items {
  display: block;
  margin-bottom: 20px;
}

.checkbox-items:nth-child(7) {
  margin-bottom: 30px;
}

.generate-btn {
  background: #a4ffaf;
  width: 100%;
  padding: 15px;
  font-size: 18px;
}

.password-strength {
  margin-bottom: 10px;
}

.bars {
  background: #24232b;
  border: 1px solid white;
  margin-bottom: 20px;
}

.bars:nth-child(n + 2) {
  margin-left: 5px;
}

.strength-bars {
  display: flex;
}
</style>