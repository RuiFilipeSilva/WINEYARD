<template>
  <div id="fromLogin">
    <div class="container">
      <div class="col-md-12 well">
        <div class="col-sm-4">
          <img
            style="width: 100%"
            src="../assets/vineyardgif.gif"
            class="img-fluid"
          />
        </div>
        <div class="container col-sm-6">
          <h1>Login</h1>
          <form v-on:submit.prevent="login()">
            <div class="form-group">
              <label for="exampleInputEmail1">Email:</label>
              <input
                type="email"
                class="form-control"
                id="exampleInputEmail1"
                aria-describedby="emailHelp"
                placeholder="Enter email"
                required
                v-model="emailLogin"
              />
              <small id="emailHelp" class="form-text text-muted"
                >We'll never share your email with anyone else.</small
              >
            </div>
            <div class="form-group">
              <label for="passwordLogin">Password:</label>
              <input
                type="password"
                class="form-control"
                id="passwordLogin"
                placeholder="Password"
                v-model="passwordLogin"
              />
            </div>
            <button
              id="loginBtn"
              style="
                color: white;
                text-decoration: none;
                background-color: #555555;
              "
              type="submit"
              class="button btn-primary float-right"
            >
              Iniciar Sessão
            </button>
            <button
              id="registerBtn"
              type="button"
              class="button btn-link float-right"
            >
              <router-link
                style="color: black; text-decoration: none"
                to="/register"
                >Registar</router-link
              >
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    emailLogin: "",
    passwordLogin: "",
  }),
  created: function () {
    window.addEventListener("unload", this.saveStorage);
    if (localStorage.getItem("loggedUser")) {
      this.$store.state.loggedUser = JSON.parse(
        localStorage.getItem("loggedUser")
      );
    }
    if (localStorage.getItem("users")) {
      this.$store.state.users = JSON.parse(localStorage.getItem("users"));
    }
  },
  methods: {
    login() {
      this.$store.commit("LOGIN", {
        emailLogin: this.emailLogin,
        passwordLogin: this.passwordLogin,
      });
    },
  },
  saveStorage() {
    localStorage.setItem("users", JSON.stringify(this.$store.state.users));
  },
};
</script>

<style>
.button {
  background-color: #555555; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  font-family: "Cinzel", serif;
}
#fromLogin {
  margin-top: 100px;
}

/*Align text with image*/
.well {
  display: flex;
  align-items: center;
}

.button:hover {
  background-color: #689666;
}

#registerBtn {
  font-family: "Cinzel", serif;
  background-color: white;
  border: none;
}
h1 {
  font-family: "Cinzel", serif;
}

label {
  font-family: "Raleway", sans-serif;
}

@import url("https://fonts.googleapis.com/css?family=Cinzel&display=swap");

@import url("https://fonts.googleapis.com/css?family=Didact+Gothic&display=swap");

@import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,300;0,400;1,300&display=swap");
</style>
