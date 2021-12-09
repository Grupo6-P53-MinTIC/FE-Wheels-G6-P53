<template>
<div class="row justify-content-end me-lg-5 pe-lg-4 m-2">
    <div class="col-lg-4 col-sm-6 borderR bg-light bg-gradient bg-opacity-50">
      <h2 class="text-center"><b>Registrate</b></h2>
      <br>
      <form v-on:submit.prevent="registerUser" class="">
        <div class="mb-3">
          <input
            class="inputR"
            type="email"
            placeholder="Correo electronico"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.username"
            type="text"
            placeholder="Nombre de usuario"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.password1"
            type="password"
            placeholder="Contraseña"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.password2"
            type="password"
            placeholder="Confirma contraseña"
          />
        </div>
        <h4 class="text-center"><b>informacion personal</b></h4>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.name"
            type="text"
            placeholder="nombre del pasagero"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.lastName"
            type="text"
            placeholder="apellido del pasagero"
          />
        </div>
        <p class="text-center">fecha de nacimiento:</p>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.birthDate"
            type="datetime-local"
            id="meeting-time"
            name="meeting-time"
            min="2021-10-31T17:22:29Z"
            max="2030-10-31T17:22:29Z"
          />
        </div>
        <select v-model="userP.gender"  class="form-control" id="GenderInput">
          <option value="">genero</option>
          <option value="M">Maculino</option>
          <option value="F">Femenino</option>
        </select>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.documentNumber"
            type="text"
            placeholder="numero de documento"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="userP.phoneNumber"
            type="text"
            placeholder="numero telefonico"
          />
        </div>
        <h4 class="text-center"><b>Tipo de usuario</b></h4>

        <div class="mb-3">
          <b-button v-b-toggle.my-collapse>Conductor</b-button>
          <b-button>Pasagero</b-button>
        </div>
<!-- BOTONES DE BOOSTRAP -->
        <b-collapse id="my-collapse">
          <b-card title="Collapsible card">
            <div class="mb-3">
              <input
                class="inputR"
                v-model="car.carRegistrationNumber"
                type="text"
                placeholder="placa del automobil"
              />
            </div>
          </b-card>
        </b-collapse>



        
        <div class="mb-3">
          <input
            class="inputR"
            v-model="car.licenseNumber"
            type="text"
            placeholder="numero de licencia de conduccion"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="car.color"
            type="text"
            placeholder="color del vehiculo"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="car.brand"
            type="text"
            placeholder="marca del vehiculo"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="car.model"
            type="text"
            placeholder="modelo del vehiculo"
          />
        </div>
        <div class="mb-3">
          <input
            class="inputR"
            v-model="car.description"
            type="text"
            placeholder="descripcion del vehiculo"
          />
        </div>

        <div class="mb-3">
          <p class="text-center">¿Ya tienes una cuenta?</p>
          <p class="text-center mt-0" v-on:click="loadLogin">
            <a href="">Inicia sesión</a>
          </p>
          <p v-if="error" class="errorMessage text-center">
            Las contraseñas no coinciden
          </p>
        </div>
        <div class="text-center">
          <button type="submit" class="btn btn-primary buttonR w-lg-50">
            Registrate
          </button>
        </div>
      </form>
    </div>
  </div>
  <div class="register">
    <div class="container_register">
      <h2><b>Registrate</b></h2>
      <form v-on:submit.prevent="registerUser">
        <input type="email" placeholder="Correo electronico" />
        <br />
        <input
          v-model="user.username"
          type="text"
          placeholder="Nombre de usuario"
        />
        <br />
        <input
          v-model="user.password1"
          type="password"
          placeholder="Contraseña"
        />
        <br />
        <input
          v-model="user.password2"
          type="password"
          placeholder="Confirmar contraseña"
        />
        <br />
        <p>¿Ya tienes una cuenta?</p>
        <p v-on:click="successRegister" ><a href="">Inicia sesión</a></p>
        <br />
        <p v-if="error" class="errorMessage">Las contraseñas no coinciden</p>
        <button type="submit">Registrar</button>
      </form>
    </div>
  </div> -->
</template>

<script>
import axios from "axios";

export default {
  name: "register",
  data: function () {
    return {
      userP: {
        username: "",
        password: "",
        password2: "",
        email: "",
        name:"",
        lastName:"",
        birthDate:"",
        gender:"",
        documentNumber:"",
        phoneNumber:"",
        typeAccount:""
      },
      car:{
        carRegistrationNumber:"",
        licenseNumber:"",
        color:"",
        brand:"",
        model:"",
        description:"",
        equipament:""
      },
      Driver: false,
      error:  false,
    };
  },
  methods: {
    registerUser: function () {
      let url = "https://wheelsapp.herokuapp.com/rest-auth/registration/";
      let body = this.user;
      let config = { headers: {} };
      axios
        .post(url, body, config)
        .then((result) => {
          this.error = false;
          console.log(result);
          this.$emit("success", result);
          this.$emit("successRegister", result);
        })
        .catch((error) => {
          this.error = true;
          console.log(error);
        });
    },
  },
  created: function () {

  },
};
</script>

