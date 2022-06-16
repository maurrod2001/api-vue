<template>
    <h1>{{ msg }}</h1>
    <div class="container mt-5">
        <div class="row">
            <div class="col-lg-6">
                <h3>Consultar todos</h3>
                <!--Consultar todos los registros. llama el metodo getall()-->
                <button class="btn btn-primary" @click="getAll()">Buscar todos</button>
            </div>
            <div class="col-lg-6">
                <h3>Consultar por nombre</h3>
                <!--Consultar por Id. llama el metodo getallbyid()-->
                <input type="text" id="txtid" class="form-control" placeholder="Nombre" />
                <br />
                <button class="btn btn-primary" @click="getAllById()">
                    Buscar por Nombre
                </button>
            </div>
        </div>
        <br />

        <hr />

        <div class="row">
            <div class="col-lg-6">
                <h3>Insertar o actualizar un contacto</h3>
                <!--operacion pa-->
                <input type="text" id="txtnombre" class="form-control" placeholder=" Nombre " /><br />
                <input type="text" id="txtlastname" class="form-control" placeholder="apellido" /><br />
                <input type="text" id="txtemail" class="form-control" placeholder=" Email " /><br />
                <input type="text" id="txttel" class="form-control" placeholder=" Telefono " /><br />

                <button class="btn btn-info me-5" @click="add_contact()">
                    Insertar un medico
                </button>
                <button class="btn btn-warning" @click="update()">
                    Actualizar un medico
                </button>
            </div>

            <br />
            <div class="col-lg-12 mt-5 table-responsive-sm">
                <table class="table table-dark bg-dark table-bordered table-hover table-striped">
                    <tr>
                        <th>nombre</th>
                        <th>apellido</th>
                        <th>correo</th>
                        <th>tel</th>
                    </tr>

                    <tbody>
                        <tr v-for="(pacient, index) in medics" :key="index">
                            <td>{{ pacient.name }}</td>
                            <td>{{ pacient.lastname }}</td>
                            <td>{{ pacient.email }}</td>
                            <td>{{ pacient.phone }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: "medicapi",

    props: {
        msg: String,
    },
    data() {
        return {
            medics: [],
        };
    },
    created() {
        this.getAll();
    },

    methods: {
        getAll() {
            axios
                .get("http://localhost:3000/medic")
                .then((response) => {
                    // for (var i = 0; i < test; i++) {
                    //     alert(response.data[i].name)

                    // }
                    // console.log(response.data)
                    // let test= response.data
                    // console.log(test)
                    this.medics = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },

        getAllById() {
            let no = document.getElementById("txtid").value;
            axios
                .get("http://localhost:3000/medic/" + no)
                .then((response) => {
                    console.log(response);
                    console.log(response.data[0].name);
                    alert(response.data[0].name);
                    this.medics = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
        },

        ///////////////////funcion para la ruta para insertar
        add_contact() {
            let txtnombre = document.getElementById("txtnombre").value;
            let txtlastname = document.getElementById("txtlastname").value;
            let txtemail = document.getElementById("txtemail").value;
            let txttel = document.getElementById("txttel").value;
            const nuevocontacto = {
                name: txtnombre,
                lastname: txtlastname,
                email: txtemail,
                phone: txttel,
            };

            axios({
                method: "POST",
                url: "http://localhost:3000/medic",
                data: nuevocontacto,
            })
                .then((res) => console.log(res), alert("Contacto agregado."))
                .catch((err) => console.log("Error: ", err));
            console.log(this.getAll());
        },

        ///////////////////funcion para actualizar
        update() {
            let txtnombre = document.getElementById("txtnombre").value;
            let txtlastname = document.getElementById("txtlastname").value;
            let txtemail = document.getElementById("txtemail").value;
            let txttel = document.getElementById("txttel").value;
            const nuevocontacto = {
                name: txtnombre,
                lastname: txtlastname,
                email: txtemail,
                phone: txttel,
            };

            axios({
                method: "PUT",
                url: "http://localhost:3000/medic/" + txtnombre,
                data: nuevocontacto,
            })
                .then((res) => console.log(res), alert("medic updated."))
                .catch((err) => console.log("Error: ", err));
            console.log(this.getAll());
        },

        ///////////////////funcion para eliminar
        delete_contact() {
            let id = document.getElementById("txtid_eli").value;

            axios
                .delete("http://localhost:3000/pacient/" + id)
                .then((res) => {
                    console.log(res.data);

                    alert(" paciente borrado.");
                })
                .catch((err) => console.log("Error: ", err));
        },
    },
};
</script>

<style scoped>
</style>
