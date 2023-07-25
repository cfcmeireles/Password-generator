<template>
  <div id="password-generator">
    <div class="generated-password" data-placeholder="P4$5W0rD?">
      {{ password.newPassword.join("") }}
    </div>
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
        @change="logSelectedRequirements"
      >
        <input
          type="checkbox"
          v-model="requirement.isChecked"
          @change="passwordStrength(index)"
        />
        {{ requirement.text }}
      </div>
      <div class="strength-display">
        <div class="password-strength">
          {{ password.strength }}
        </div>
        <div
          class="bars"
          v-for="(bar, index) in 4"
          :key="index"
          :style="passwordStrength(index)"
          style="height: 24px; width: 2%"
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
        length: 12,
        newPassword: [],
        buttonClicked: false,
        showAlert: false,
        strength: "",
        result: [],
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
      console.log("checkedRequirements:", this.checkedRequirements.length);
    },
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
          this.password.result.push(req[randomValue]);
        });
      }
      console.log(this.password.result);
      let missingRequiredCharacters;
      for (var j = 0; j < this.checkedRequirements.length; j++) {
        missingRequiredCharacters = this.checkedRequirements[
          j
        ].characters.every(
          (element) => !this.password.result.includes(element)
        );
      }
      if (missingRequiredCharacters) {
        {
          this.password.result = [];
          this.generatePassword();
        }
      }
      this.password.newPassword.push(this.password.result.join(""));
      this.password.result = [];
    },
    passwordStrength(index) {
      if (index < this.checkedRequirements.length) {
        return {
          backgroundColor: "#F3CD6C",
        };
      }
      let strengthText = ["WEAK", "MEDIUM", "MEDIUM", "STRONG"];
      let reqIndex = this.checkedRequirements.length;
      if (!reqIndex) {
        this.password.strength = "STRENGTH";
      } else {
        for (let i = 0; i < reqIndex; i++) {
          this.password.strength = strengthText[reqIndex];
        }
      }
    },
  },
};
</script>
  
<style>
.generated-password {
  background: #24232b;
  height: 60px;
  margin-bottom: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 540px;
}

div:empty:before {
  content: attr(data-placeholder);
  color: gray;
}

.main-div {
  background: #24232b;
  height: 500px;
  width: 500px;
  padding: 20px;
}

.password-range {
  margin-bottom: 30px;
  width: 100%;
}

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

.strength-display {
  background: #121117;
  height: 60px;
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}

.password-strength {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.bars {
  background: #24232b;
  border: 1px solid white;
  margin-top: 12px;
}

.bars:nth-child(n + 2) {
  margin-left: 5px;
}

.strength-bars {
  display: flex;
}

@media only screen and (max-width: 500px) {
  .generated-password {
    width: 340px;
  }

  .main-div {
    width: 300px;
  }
}

@media only screen and (min-width: 501px) and (max-width: 600px) {
  .generated-password {
    width: 440px;
  }

  .main-div {
    width: 400px;
  }
}
</style>