<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-lg-6">
                <h3>Consultar todos</h3>
                <!--Consultar todos los registros. llama el metodo getall()-->
                <button class="btn btn-primary" @click="getAll()">Buscar todos</button>
            </div>
            <div class="col-lg-6">
                <h3>Consultar por id</h3>
                <!--Consultar por Id. llama el metodo getallbyid()-->
                <input type="text" id="txtid" class="form-control" placeholder="Id"> <br>
                <button class="btn btn-primary" @click="getAllById()">Buscar por Id</button>
            </div>

        </div>
        <br>


        <hr>





        <div class="row">
            <div class="col-lg-6">
                <h3>Insertar un contacto</h3>
                <!--operacion pa-->
                <input type="text" id="txtnombre" class="form-control" placeholder=" Nombre "><br>
                <input type="text" id="txttel" class="form-control" placeholder=" Telefono "><br>
                <input type="text" id="txtemail" class="form-control" placeholder=" Email "><br>
                <button class="btn btn-warning" @click="add_contact()">Insertar un contacto</button>

            </div>
            <div class="col-lg-6">
                <h3>Actualizar un contacto</h3>
                <!--operacion pa-->
                <input type="text" id="txtnombre_act" class="form-control" placeholder=" Nombre "><br>
                <input type="text" id="txttel_act" class="form-control" placeholder=" Telefono "><br>
                <input type="text" id="txtemail_act" class="form-control" placeholder=" Email "><br>
                <input type="text" id="txtid_act" class="form-control" placeholder=" Id "><br>
                <button class="btn btn-warning" @click="update()">Actualizar un contacto</button>
            </div>

        </div>


        <hr>

        <div class="row">
            <div class="col-lg-6">
                <h3>Eliminar por id</h3>
                <!--operacion para consultar todos. llama el metodo getallbyid()-->
                <input type="text" id="txtid_eli" class="form-control" placeholder="Id "> <br>
                <button class="btn btn-danger" @click="delete_contact()">Eliminar un contacto</button>
            </div>
            <div class="col-lg-6">

            </div>

        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name: 'api',
    data() {

        return {

        }
    },

    methods: {
        getAll() {
            axios.get('http://localhost:3000/getAll')
                .then(function (response) {
                    console.log(response);
                    console.log(response.data[length].fullname);
                    var test = response.data.length
                    console.log(test)
                    for (var i = 0;i < test; i++) {
                        alert(response.data[i].fullname)
                    }

                })
                .catch(function (error) {
                    console.log(error);
                });
        }










        , getAllById() {
            let id = document.getElementById("txtid").value;
            // id = this.$refs.txtid
            //  var id = 1
            // id = this.$refs.txtid
            axios.get('http://localhost:3000/getAllById/' + id)
                .then(function (response) {
                    console.log(response);
                    console.log(response.data[0].fullname);
                    alert(response.data[0].fullname);
                })
                .catch(function (error) {
                    console.log(error);
                });
        }





        ///////////////////funcion para la ruta para insertar
        , add_contact() {
            let txtnombre = document.getElementById("txtnombre").value;
            let txttel = document.getElementById("txttel").value;
            let txtemail = document.getElementById("txtemail").value;
            const nuevocontacto = {
                fullname: txtnombre,
                phone: txttel,
                email: txtemail
            }

            axios({
                method: 'POST',
                url: 'http://localhost:3000/add_contact',
                data: nuevocontacto,
            }).then(res => console.log(res), alert("Contacto agregado."))
                .catch(err => console.log('Error: ', err))
        }




        ///////////////////funcion para actualizar
        , update() {
            let txtnombre = document.getElementById("txtnombre_act").value;
            let txttel = document.getElementById("txttel_act").value;
            let txtemail = document.getElementById("txtemail_act").value;
            let id = document.getElementById("txtid_act").value;
            const nuevocontacto = {
                fullname: txtnombre,
                phone: txttel,
                email: txtemail
            }

            axios({
                method: 'PUT',
                url: 'http://localhost:3000/update/' + id,
                data: nuevocontacto,
            }).then(res => console.log(res), alert("Contacto actualizado."))
                .catch(err => console.log('Error: ', err))
        }





        ///////////////////funcion para eliminar
        , delete_contact() {

            let id = document.getElementById("txtid_eli").value;

            axios.delete('http://localhost:3000/delete/' + id)
                .then(res => {
                    console.log(res.data)

                    alert("Contacto actualizado.")



                })
                .catch(err => console.log('Error: ', err))
        }



    }

}
</script>


<style scoped>
</style>