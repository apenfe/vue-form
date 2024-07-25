<template>

    <section>

        <h3>Añadir profesor</h3>

        <div>
            <label>Nombre:</label>
            <input type="text" v-model="teacher.teacherName">
        </div>

        <div>
            <label>Apellidos:</label>
            <input type="text" v-model="teacher.teacherSurname">
        </div>

        <div>
            <label>DNI:</label>
            <input type="text" v-model="teacher.dni">
        </div>

        <div>
            <label>Materias:</label>
            <input type="text" v-model="subject" >
            <button @click="handleSubject()">Añadir Materia</button>
        </div>

        <div>
            <ul>
                <li v-for="(elm,index) in teacher.subjects" :key="index">
                    <h4>{{elm}}</h4>
                </li>
            </ul>
        </div>

        <input type="checkbox" v-model="teacher.doc"> Documentacion entregada.
        <button @click="handleAddTeacher()">Añadir Profesor</button>

    </section>

    <section>

        <h3>Listado de profesores</h3>

        <table>

            <tr>
                <th>Nombre</th>
                <th>Apellidos</th>
                <th>DNI</th>
                <th>Asignaturas</th>
                <th>Documentacion</th>
            </tr>

            <tr v-for="(elm,index) in teachers" :key="index">
                <th>{{elm.teacherName}}</th>
                <th>{{elm.teacherSurname}}</th>
                <th>{{elm.dni}}</th>
                <th>
                    <ul>
                        <li v-for="(item,index) in elm.subjects" :key="index">
                            {{item}}
                        </li>
                    </ul>
                </th>
                <th v-if="elm.doc">Entregada</th>
                <th v-else>Falta</th>
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

</style>