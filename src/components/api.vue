<template>
    <h1> {{ msg }} </h1>
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
                <input type="text" id="txtid" class="form-control" placeholder="Id"> <br>
                <button class="btn btn-primary" @click="getAllById()">Buscar por Id</button>
            </div>

        </div>
        <br>


        <hr>





        <div class="row">
            <div class="col-lg-6">
                <h3>Insertar o actualizar un contacto</h3>
                <!--operacion pa-->
                <input type="text" id="txtno" class="form-control" placeholder="numero"><br>
                <input type="text" id="txtnombre" class="form-control" placeholder=" Nombre "><br>
                <input type="text" id="txtlastname" class="form-control" placeholder="apellido"><br>
                <select class="form-select" aria-label="Default select example" id="txtgender">
                    <option selected>genero</option>
                    <option value="m">male</option>
                    <option value="f">female</option>

                </select><br>
                <input type="date" id="txtdob" class="form-control"><br>
                <input type="text" id="txtemail" class="form-control" placeholder=" Email "><br>
                <input type="text" id="txttel" class="form-control" placeholder=" Telefono "><br>
                <textarea name="" class="form-control" id="txtmedic" cols="30" rows="3"
                    placeholder="medicamentos prescritos"></textarea><br>
                <textarea name="" class="form-control" id="txtaler" cols="30" rows="3"
                    placeholder="alergias del paciente"></textarea><br>

                <button class="btn btn-info me-5" @click="add_contact()">Insertar un contacto</button>
                <button class="btn btn-warning" @click="update()">Actualizar un contacto</button>

            </div>


            <br>
            <div class="col-lg-12 mt-5">
                <table class="table  table-dark bg-dark  table-hover table-striped ">
                    <tr>
                        <th>numero</th>
                        <th>nombre</th>
                        <th>apellido</th>
                        <th>genero</th>
                        <th>cumpleaños</th>
                        <th>correo</th>
                        <th>tel</th>
                        <th>medicamentos</th>
                        <th>alergias</th>
                        <th>eliminar</th>


                    </tr>

                    <tbody>
                        <tr v-for="(pacient, index) in pacients" :key="index">
                            <td id="test+pacient">{{ pacient.no }}</td>
                            <td> {{ pacient.name }} </td>
                            <td> {{ pacient.lastname }} </td>
                            <td> {{ pacient.gender }} </td>
                            <td> {{ pacient.day_of_birth }} </td>
                            <td> {{ pacient.email }} </td>
                            <td> {{ pacient.phone }} </td>
                            <td> {{ pacient.medicaments }} </td>
                            <td> {{ pacient.alergy }} </td>
                             <td><button class="btn btn-danger" @click="delete_contact(index)">delete</button> </td>


                        </tr>
                    </tbody>




                </table>

            </div>

        </div>


        <button type="submit" class="btn btn-danger" >delete</button>

    </div>
</template>

<script>
import axios from "axios";
export default {
    name: 'api',

    props: {
        msg: String
    },
    data() {


        return {
            pacients: []
        };
    },
    created() {
        this.getAll();
    },


    methods: {
        getAll() {
            axios.get('http://localhost:3000/pacient')
                .then((response) => {
                    // for (var i = 0; i < test; i++) {
                    //     alert(response.data[i].name)

                    // }
                    // console.log(response.data)
                    // let test= response.data
                    // console.log(test)
                    this.pacients = response.data

                })
                .catch((error) => {
                    console.log(error);
                });
        },










        getAllById() {
            let no = document.getElementById("txtid").value;
            axios.get('http://localhost:3000/pacient/' + no)
                .then((response) => {
                    console.log(response);
                    console.log(response.data[0].name);
                    alert(response.data[0].name)
                    this.pacients = response.data


                })
                .catch((error) => {
                    console.log(error);
                });
        }





        ///////////////////funcion para la ruta para insertar
        , add_contact() {
            let txtno = document.getElementById("txtno").value
            let txtnombre = document.getElementById("txtnombre").value;
            let txtlastname = document.getElementById("txtlastname").value;
            let txtgender = document.getElementById("txtgender").value;
            let txtdob = document.getElementById("txtdob").value
            let txtemail = document.getElementById("txtemail").value;
            let txttel = document.getElementById("txttel").value;
            let txtmedic = document.getElementById("txtmedic").value;
            let txtaler = document.getElementById("txtaler").value
            const nuevocontacto = {
                no: txtno,
                name: txtnombre,
                lastname: txtlastname,
                gender: txtgender,
                day_of_birth: txtdob,
                email: txtemail,
                phone: txttel,
                medicaments: txtmedic,
                alergy: txtaler

            }

            axios({
                method: 'POST',
                url: 'http://localhost:3000/pacient',
                data: nuevocontacto,
            }).then(res => console.log(res), alert("Contacto agregado."))
                .catch(err => console.log('Error: ', err))
            console.log(this.getAll())

        }




        ///////////////////funcion para actualizar
        , update() {
            let txtno = document.getElementById("txtno").value
            let txtnombre = document.getElementById("txtnombre").value;
            let txtlastname = document.getElementById("txtlastname").value;
            let txtgender = document.getElementById("txtgender").value;
            let txtdob = document.getElementById("txtdob").value
            let txtemail = document.getElementById("txtemail").value;
            let txttel = document.getElementById("txttel").value;
            let txtmedic = document.getElementById("txtmedic").value;
            let txtaler = document.getElementById("txtaler").value
            const nuevocontacto = {
                no: txtno,
                name: txtnombre,
                lastname: txtlastname,
                gender: txtgender,
                day_of_birth: txtdob,
                email: txtemail,
                phone: txttel,
                medicaments: txtmedic,
                alergy: txtaler

            }

            axios({
                method: 'PUT',
                url: 'http://localhost:3000/pacient/' + txtno,
                data: nuevocontacto,

            }).then(res => console.log(res), alert("pacient updated."))
                .catch(err => console.log('Error: ', err))
            console.log(this.getAll())

        }





        ///////////////////funcion para eliminar
        , delete_contact(index  ) {

            let id = document.getElementById("txtid_eli").value;

            axios.delete('http://localhost:3000/pacient/' + index)
                .then(res => {
                    console.log(res.data)

                    alert(" paciente borrado.")



                })
                .catch(err => console.log('Error: ', err))
        }



    }

}
</script>


<style scoped>
</style>