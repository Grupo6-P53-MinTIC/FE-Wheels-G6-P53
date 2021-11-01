<template>
  <div class="bc_patron">
    <div class="row bg-secondary bg-light bg-opacity-50" >
      <div class="col-5 blur shadow-lg p-3 bg-body rounded border-dark me-3" v-for="dataTravel in travels">
        <form v-on:submit.prevent="editTravel">
          <table class="table table-striped table-hover">
            <thead>
              <tr>
                <th scope="col" class="fs-5">{{ dataTravel.from_place }} <i class="fas fa-long-arrow-alt-right"></i>
            {{ dataTravel.to_place }}</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th scope="row">Desde</th>
                <td v-if="!edit_from_place">{{ dataTravel.from_place }}</td>
                <td v-if="edit_from_place">
                   <input type="text" v-model="dataTravel.from_place"/>
                </td>
                <td>
                  <i
                    @click="edit_from_place = !edit_from_place"
                    class="fas fa-pen"
                  ></i>
                </td>
              </tr>
              <tr>
                <th scope="row">Hasta</th>
                <td v-if="!edit_to_place">{{ dataTravel.to_place }}</td>
                <td v-if="edit_to_place">
                  <input type="text" v-model="dataTravel.to_place" />
                </td>

                <td>
                  <i
                    @click="edit_to_place = !edit_to_place"
                    class="fas fa-pen"
                  ></i>
                </td>
              </tr>
              <tr>
                <th scope="row">Pasa por</th>
                <td v-if="!edit_pass_through">{{ dataTravel.pass_through }}</td>
                <td v-if="edit_pass_through">
                  <input type="text" v-model="dataTravel.pass_through" />
                </td>

                <td>
                  <i
                    @click="edit_pass_through = !edit_pass_through"
                    class="fas fa-pen"
                  ></i>
                </td>
              </tr>
              <tr>
                <th scope="row">Asientos disponibles</th>
                <td v-if="!edit_seats">{{ dataTravel.seats }}</td>
                <td v-if="edit_seats">
                  <input type="text" v-model="dataTravel.seats" />
                </td>

                <td>
                  <i @click="edit_seats = !edit_seats" class="fas fa-pen"></i>
                </td>
              </tr>
              <tr>
                <th scope="row">Sale</th>
                <td v-if="!edit_date_travel">{{ dataTravel.date_travel }}</td>
                <td v-if="edit_date_travel">
                  <input
                    v-model="dataTravel.date_travel"
                    type="datetime-local"
                    id="meeting-time"
                    name="meeting-time"
                    min="2021-10-31T17:22:29Z"
                    max="2030-10-31T17:22:29Z"
                  />
                </td>

                <td>
                  <i
                    @click="edit_date_travel = !edit_date_travel"
                    class="fas fa-pen"
                  ></i>
                </td>
              </tr>
              <tr>
                <th scope="row">Precio</th>
                <td v-if="!edit_price">COP ${{ dataTravel.price }}</td>
                <td v-if="edit_price">
                  <input type="text" v-model="dataTravel.price" />
                </td>

                <td>
                  <i @click="edit_price = !edit_price" class="fas fa-pen"></i>
                </td>
              </tr>
            </tbody>
            <div class="text-center p-2">
              <button class="btn btn-primary buttonR" type="submit">
              <b>Guardar cambios</b>
            </button>
            </div>
          </table>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "editTravel",
  data: function () {
    return {
      idUser: [],
      travels: [],
      edit_from_place: false,
      edit_to_place: false,
      edit_pass_through: false,
      edit_date_travel: false,
      edit_seats: false,
      edit_price: false,
    };
  },
  methods: {
    getUser: function () {
      let url = "https://wheelsapp.herokuapp.com/rest-auth/user/";
      let config = {
        headers: { Authorization: `Token ${localStorage.getItem("token")}` },
      };
      axios
        .get(url, config)
        .then((res) => {
          this.idUser = res.data.pk;
          this.getTravel(this.idUser);
        })
        .catch((e) => console.log(e));
    },
    getTravel: function (id) {
      let url = `https://wheelsapp.herokuapp.com/travel_by/${id}`;
      let config = {
        headers: { Authorization: `Token ${localStorage.getItem("token")}` },
      };
      axios
        .get(url, config)
        .then((res) => {
          this.travels = res.data;
          console.log(res.data);
        })
        .catch((e) => console.log(e));
    },
    editTravel: function (id) {
      let url = `https://wheelsapp.herokuapp.com/travel/${this.dataTravel.id}`;
      let body = this.dataTravel;
      let config = {
        headers: { Authorization: `Token ${localStorage.getItem("token")}` },
      };
      axios
        .put(url, body, config)
        .then((result) => {
          this.$emit("success", result);
        })
        .catch((error) => {
          this.error = true;
          console.log(error);
        });
    },
  },
  created: function () {
    this.getUser();
  },
};
</script>