<template>
  <div class="background">
    <div class="container">
      <div class="window">
        <div class="overlay"></div>
        <div class="content">
          <div class="welcome">RESET-PASSWORD</div>
          <div class="subtitle">
            Enter new password to reset your forgoten one
          </div>

          <div class="input-fields">
            <input
              type="password"
              placeholder="Password"
              class="input-line full-width"
              v-model="password"
            />
            <input
              type="password"
              placeholder=" confirm Password"
              class="input-line full-width"
              v-model="confirmPassword"
            />
          </div>

          <div>
            <button @click="handleSubmit()" class="ghost-round full-width">
              Submit Password
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const apiUrl = process.env.API_URL || "https://mzansi-curator.herokuapp.com/";

export default {
  name: "reset-password",
  data() {
    return {
      password: "",
      confirmPassword: "",
      code: this.$route.query.code,
    };
  },
  methods: {
    async handleSubmit() {
      try {
        const {data} = await axios.post(`${apiUrl}/auth/reset-password`, {
          code: this.code, 
          password: this.password,
          passwordConfirmation: this.confirmPassword,
        });
        this.$store.commit("setUser", data);
        this.$router.push('/')
      } catch (err) {
        console.log(err.message);
      }
    },
  },
};
</script>

<style lang="css" scoped>
input {
  border: none;
}

button:focus {
  outline: none;
}

::-webkit-input-placeholder {
  color: rgba(255, 255, 255, 0.65);
}

::-webkit-input-placeholder .input-line:focus + ::input-placeholder {
  color: #fff;
}

.highlight {
  color: rgba(255, 255, 255, 0.8);
  font-weight: 400;
  cursor: pointer;
  transition: color 0.2s ease;
}

.highlight:hover {
  color: #fff;
  transition: color 0.2s ease;
}

.spacing {
  -webkit-box-flex: 1;
  -webkit-flex-grow: 1;
  -ms-flex-positive: 1;
  flex-grow: 1;
  font-weight: 300;
  text-align: center;
  margin-top: 10px;
  color: rgba(255, 255, 255, 0.65);
}

.input-line:focus {
  outline: none;
  border-color: #fff;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}

.ghost-round {
  cursor: pointer;
  background: none;
  border: 1px solid rgba(255, 255, 255, 0.65);
  border-radius: 25px;
  color: rgba(255, 255, 255, 0.65);
  -webkit-align-self: flex-end;
  -ms-flex-item-align: end;
  align-self: flex-end;
  font-size: 19px;
  font-size: 1.2rem;
  font-family: roboto;
  font-weight: 300;
  line-height: 2em;
  margin-top: auto;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}

.ghost-round:hover {
  background: rgba(255, 255, 255, 0.15);
  color: #fff;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}

.input-line {
  background: none;
  margin-bottom: 10px;
  line-height: 2.4em;
  color: #fff;
  font-family: roboto;
  font-weight: 300;
  letter-spacing: 0px;
  letter-spacing: 0.02rem;
  font-size: 19px;
  font-size: 1.2rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.65);
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}

.full-width {
  width: 100%;
}

.input-fields {
  margin-top: 25px;
}

.container {
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  -ms-flex-align: center;
  align-items: center;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  -ms-flex-pack: center;
  justify-content: center;
  background: #eee;
  height: 650px;
}

.content {
  padding-left: 25px;
  padding-right: 25px;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-flow: column;
  -ms-flex-flow: column;
  flex-flow: column;
  z-index: 1;
}

.welcome {
  font-weight: 200;
  margin-top: 15px;
  text-align: center;
  font-size: 40px;
  font-size: 2.5rem;
  letter-spacing: 0px;
  letter-spacing: 0.05rem;
}

.subtitle {
  text-align: center;
  line-height: 1em;
  font-weight: 100;
  letter-spacing: 0px;
  letter-spacing: 0.02rem;
}

.window {
  color: #fff;
  font-family: roboto;
  position: relative;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-flow: column;
  -ms-flex-flow: column;
  flex-flow: column;
  box-shadow: 0px 15px 50px 10px rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  height: 500px;
  width: 360px;
  background: #fff;
}

.overlay {
  background: -webkit-linear-gradient(#8ca6db, #b993d6);
  background: linear-gradient(#8ca6db, #b993d6);
  filter: alpha(opacity=85);
  height: 500px;
  position: absolute;
  width: 360px;
}
</style>
