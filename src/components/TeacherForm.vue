<template>

    <section id="form">

        <h3>Añadir profesor</h3>

        <div id="data">

            <div>
                <label>Nombre:</label>
                <input type="text" v-model="teacher.teacherName">
            </div>
    
            <div class="clearfix"></div>
        
            <div>
                <label>Apellidos:</label>
                <input type="text" v-model="teacher.teacherSurname">
            </div>
    
            <div class="clearfix"></div>

            <div>
                <label>DNI:</label>
                <input type="text" v-model="teacher.dni">
            </div>
    
            <div class="clearfix"></div>

            <div>
                <label>Materias:</label>
                <input id="materias" type="text" v-model="subject" >
                <button @click="handleSubject()">Añadir Materia</button>
            </div>
    
            <div class="clearfix"></div>

            <div id="listado">
                <ul>
                    <li v-for="(elm,index) in teacher.subjects" :key="index">
                        <h4>{{elm}}</h4>
                    </li>
                </ul>
            </div>
    
            <div class="clearfix"></div>

            <div>
                <input id="check" type="checkbox" v-model="teacher.doc"> 
                <h4>Documentacion entregada.</h4>
                <button id="addteacher" @click="handleAddTeacher()">Añadir Profesor</button>
            </div>

            <div class="clearfix"></div>

        </div>

    </section>

    <section id="lista">

        <h3>Listado de profesores</h3>

        <table id="tabla">

            <thead id="encabezado">
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>DNI</th>
                <th>Asignaturas</th>
                <th>Documentacion</th>
            </thead>

            <div class="clearfix"></div>

            <tr id="content" v-for="(elm,index) in teachers" :key="index">
                <td>{{elm.teacherName}}</td>
                <td>{{elm.teacherSurname}}</td>
                <td>{{elm.dni}}</td>
                <td>
                    <ul id="sublistado">
                        <li v-for="(item,index) in elm.subjects" :key="index">
                            {{item}}
                        </li>
                    </ul>
                </td>
                <td v-if="elm.doc">Entregada</td>
                <td v-else>Falta</td>
            </tr>

        </table>
        
    </section>
   
</template>

<script lang="ts" setup>

    import {Ref, ref} from 'vue';

    interface ITeacher {
        teacherName: string,
        teacherSurname: string,
        dni: string,
        subjects: Array<string>,
        doc: boolean
    }

    let teacher:Ref<ITeacher> = ref({
        teacherName: '',
        teacherSurname: '',
        dni: '',
        subjects: [],
        doc: false

    });

    let teachers:Ref <Array<ITeacher>> = ref([]);

    let subject:Ref<string> = ref('');

    const handleSubject = () => {

        teacher.value.subjects.push(subject.value);

        subject.value = "";
    }

    const handleAddTeacher = () => {

        teachers.value.push({
            teacherName: teacher.value.teacherName,
            teacherSurname: teacher.value.teacherSurname,
            dni: teacher.value.dni,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        });

        teacher.value.teacherName = "";
        teacher.value.teacherSurname = "";
        teacher.value.dni = "";
        teacher.value.subjects = [];
        teacher.value.doc = false;
    }

</script>

<style scoped>

    /* ESTILOS GENERALES */

    *{
        margin: 0px auto;
        padding: 0px;
        text-align: center;
    }

    .clearfix{
        float: none;
        clear: both;
    }

    /* ESTILOS FORMULARIO */

    /* ESTILOS GENERAL FORMULARIO */

    #form{
        font-family: Arial, Helvetica, sans-serif;
        font-size: 18px;
        height: auto;
        width: 30%;
        background-color: #ccc;
        text-align: center;
        margin: 10px auto;
        margin-top: 30px;
        padding: 10px;
        border: 1px solid black;
        border-radius: 20px;
        box-shadow: 2px 3px 5px #333;
    }

    /* TITULO FORMULARIO */

    #form h3{
        display: block;
        font-size: 20px;
        height: 25px;
        width: 95%;
        background-color: #a19c9c;
        margin: 8px auto;
        padding: 8px;
        border: 1px solid gray;
        border-radius: 10px;
        box-shadow: 2px 3px 5px rgb(102, 102, 102) inset;
        color: #333;
        transition: all 300ms;
    }

    #form h3:hover{
        font-size: 22px;
        border: 1px solid black;
        border-radius: 10px;
        box-shadow: 3px 3px 6px black inset;
        color: #333;
    }

    /* CAJA DE DATOS FORMULARIO */

    #form #data{
        
        background-color: #a19c9c;
        border-radius: 5px;
        margin: 5px;
        padding: 10px;
        box-shadow: 1px 1px 3px #333 inset;
    }

    /* CAJAS DE DATOS INTERNAS */

    #form #data div{
        display: block;
        background-color: gray;
    }

    /* LABELS CAJAS DE DATOS INTERNAS */

    #form #data div label{

        display: block;
        float: left;
        width: 25%;
        height: 20px;
        line-height: 20px;
        margin: 10px;
        
    }

     /* INPUTS CAJAS DE DATOS INTERNAS */

    #form #data div input{

        display: block;
        float: left;
        width: 60%;
        height: 20px;
        border-radius: 15px;
        line-height: 20px;
        margin: 10px;
        border: none;
        
    }

    #form #data div input:hover{

        background-color: #ccc;
        
    }

     /* LABELS CAJAS DE DATOS INTERNAS (MATERIAS)*/

    #form #data div #materias{

        display: block;
        float: left;
        width: 30%;
        height: 20px;
        border-radius: 15px;
        line-height: 20px;
        margin: 10px;
        border: none;
        margin-right: 5px;
        
    }

    /* LISTADO DE MATERIAS AÑADIDAS*/

    #listado ul{
        display: block;
        float:right;
        list-style: none;
        width: 100%;
        margin: 5px;
        background-color: rgb(236, 236, 236);
        border-radius: 30px;
    }

    #listado ul li{
        display: block;
        float: left;
        width: 30%;
        margin: 5px;
        background-color: rgb(74, 74, 255);
        text-decoration: none;
        border-radius: 100px;
        border: 1px solid black;
        box-shadow: 1px 2px 3px #333;
        color: white;
        font-size: 14px;
    }

    /* LABELS CAJAS DE DATOS INTERNAS (CHECK)*/

    #form #data div #check{

        display: block;
        float: left;
        width: 5%;
        height: 20px;
        border-radius: 15px;
        line-height: 20px;
        border: none;
        margin-right: 5px;
    }

    #form #data div h4{

        display: block;
        float: left;
        width: 50%;
        height: 20px;
        font-size: 12px;
        border-radius: 15px;
        line-height: 20px;
        margin: 10px;
    }

    #form #data div #addteacher{

        display: block;
        float: left;
        width: 30%;
        height: 20px;
        border-radius: 15px;
        line-height: 20px;
        margin: 10px;
        border: none;
        cursor: pointer;
        
    }

    #form #data div button{

        display: block;
        float: left;
        width: 25%;
        height: 20px;
        border-radius: 15px;
        line-height: 20px;
        margin: 10px;
        border: none;
        cursor: pointer;
    }

    /* ESTILOS TABLA */

    /* ESTILOS TABLA GENERAL */

    #lista{
        font-family: Arial, Helvetica, sans-serif;
        font-size: 18px;
        height: auto;
        width: 65%;
        background-color: #ccc;
        text-align: center;
        margin: 10px auto;
        margin-top: 30px;
        padding: 10px;
        border: 1px solid black;
        border-radius: 20px;
        box-shadow: 2px 3px 5px #333;
    }

    #tabla{
        border-collapse: collapse;
        width: 100%;
    }

    /* ESTILOS TABLA (TITULO)*/

    #lista h3{
        display: block;
        font-size: 20px;
        height: 25px;
        width: 95%;
        background-color: #a19c9c;
        margin: 8px auto;
        padding: 8px;
        border: 1px solid gray;
        border-radius: 10px;
        box-shadow: 2px 3px 5px rgb(102, 102, 102) inset;
        color: #333;
        transition: all 300ms;
    }

    #lista h3:hover{
        font-size: 22px;
        border: 1px solid black;
        border-radius: 10px;
        box-shadow: 3px 3px 6px black inset;
        color: #333;
    }

    /* ESTILOS TABLA (ENCABEZADO)*/

    #lista #tabla #encabezado {
        display: block;
        float: left;
        width: 100%;
        font-size: 20px;
        background-color: #333;
        color: white;
    }

    #lista #tabla #encabezado th {
        display: inline-block;
        width: 20%;
    }

    /* ESTILOS TABLA (CONTENIDO)*/

    #lista #tabla #content{

        display: block;
        float: left;
        width: 100%;
        font-size: 20px;
        background-color: #5e5e5e;
        color: white;
    }

    #lista #tabla #content td {
    
        display: inline-block;
        width: 20%;
    }

    #lista #tabla #content td #sublistado{
        text-decoration: none;
        list-style: none;
    }

    #lista #tabla #content td #sublistado li{
        display: block;
        float: left;
        width: 30%;
        margin: 5px;
        background-color: rgb(74, 74, 255);
        text-decoration: none;
        border-radius: 100px;
        border: 1px solid black;
        box-shadow: 1px 2px 3px #333;
        color: white;
        font-size: 14px;
    }

</style>