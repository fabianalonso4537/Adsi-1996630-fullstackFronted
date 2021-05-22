<template>
  <!DOCTYPE html>
  <html lang="es">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta http-equiv="X-UA-Compatible" content="ie=edge" />
      <title>Registro</title>
    </head>
    <body>
      <div class="divlogin">
        <div class="container">
          <div class="divcont">
            <form>
              <div class="mb-3"><label for="exampleInputEmail1" class="form-label">Email </label>
                <input type="email" v-model="usuario.email" class="form-control" id="exampleInputEmail1"  aria-describedby="emailHelp"/>
              </div>
              <div class="mb-3">
                <label for="exampleInputPassword1" class="form-label">Password</label>
                <input type="password" v-model="usuario.password" class="form-control" id="exampleInputPassword1"/>
              </div>
              <br>
              <button @click.prevent="ingresar">Iniciar sesión</button>
            </form>
          </div>
        </div>
      </div>
    </body>
  </html>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    usuario: {
      email: "santos.pocholo@hotmail.com",
      password: "fabianalonso_12345",
    },
  }),
  methods: {
    ingresar() {
      let me = this;
      axios.post("usuario/login", {
          email: me.usuario.email,
          password: me.usuario.password,
        })
        .then(function (response) {
          console.log(response.data);
          me.$store.dispatch("setToken", response.data);
          me.$router.push('/about')
        })
        .catch(function ({ response }) {
          console.log(response);
        });
    },
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css?family=Roboto");
html,
body {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 100vh;
  font-family: "Roboto";
  color: #333;
}

.divlogin {
  background: url(../assets/fondo.jpg) no-repeat;
  background-size: cover;
  background-position: center center;
  width: 100%;
  height: 100vh;
  display: flex;
  align-content: center;
  align-items: center;
}

.divlogin .container {
  width: 100%;
  text-align: center;
}

.divlogin .container .divcont {
  width: 100%;
  max-width: 300px;
  background: rgba(255, 255, 255, 0.7);
  padding: 20px;
  border-radius: 10px;
  display: inline-block;
}

.divlogin .container .divcont h3 {
  margin-top: 0px;
}

.divlogin .container .divcont input {
  height: 30px;
  margin: 0px;
  border: 0px;
  outline: none;
  padding: 10px;
  border-radius: 5px;
  width: 90%;
  margin-bottom: 10px;
}

.divlogin .container .divcont input.error {
  border-bottom: 3px solid red;
}

.divlogin .container .divcont button {
  margin: 0px;
  border: 0px;
  display: block;
  margin: auto;
  padding: 10px 30px;
  background: #333;
  color: #fff;
  border-radius: 5px;
  margin-bottom: 10px;
}

.divlogin .container .divcont a {
  font-size: 12px;
  margin-right: 10px;
  color: #333;
}
</style>