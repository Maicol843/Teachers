<template>
    <section>
        <h3>AÑADIR PROFESOR</h3>
        <div>
            <div class="contenido-Formulario">
                <label>Nombre:</label> <input type="text" v-model="teacher.teacherName">
            </div>
            <div class="contenido-Formulario">
                <label>Apellido:</label> <input type="text" v-model="teacher.surname">
            </div>
            <div class="contenido-Formulario">
                <label>DNI / NIF:</label> <input type="text" v-model="teacher.dni">
            </div>
            <div class="contenido-Formulario">
                <label>Materias:</label> <input type="text" v-model="subject"> <button @click="handleSubject()">Agregar</button>
            </div>
            <div class="contenido-Formulario">
                <ul>
                    <li v-for="(elm, index) in teacher.subjects" :key="index">{{ elm }}</li>
                </ul>
            </div>
            <div class="contenido-Formulario"> 
                <input type="checkbox" v-model="teacher.doc"> <span>Documentación Entregada</span>
                <button @click="handleAddTeacher()">Agregar</button>
            </div>
        </div>
    </section>

    <section>
        <h3>LISTADO DE PROFESORES</h3>
        <div class="contenedor-Tabla">
            <table>
                <tr>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>DNI / NIF</th>
                    <th>Materias</th>
                    <th>Documentación Entregada</th>
                </tr>
                <tr v-for="elm in teachers" :key="elm.dni">
                    <td>{{ elm.teacherName }}</td>
                    <td>{{ elm.surname }}</td>
                    <td>{{ elm.dni }}</td>
                    <td>
                        <ul>
                            <li v-for="(item,index) in elm.subjects" :key="index">{{ item }}</li>
                        </ul>
                    </td>
                    <td v-if="elm.doc">Entregado</td>
                    <td v-else>No entregado</td>
                </tr>
            </table>
        </div>
    </section>
</template>

<script lang="ts" setup>
    import {Ref, ref} from 'vue'
    
    interface ITeacher{
        teacherName: string,
        surname: string,
        dni: string,
        subjects: Array<string>,
        doc:boolean
    }

    let teacher:Ref<ITeacher> = ref({
        teacherName: '',
        surname: '',
        dni:'',
        subjects: [],
        doc: false
    })

    let teachers:Ref<Array<ITeacher>> = ref([])

    let subject:Ref<string> = ref('')

    const handleSubject = () => {
        teacher.value.subjects.push(subject.value)
        subject.value = "" //Me vacía el campo de materias
    }

    const handleAddTeacher = () => {
        teachers.value.push({
            teacherName: teacher.value.teacherName,
            surname: teacher.value.surname,
            dni: teacher.value.dni,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        })
        teacher.value.teacherName = ""
        teacher.value.surname = ""
        teacher.value.dni = ""
        teacher.value.subjects = []
        teacher.value.doc = false
    }
</script>

<style scoped>
    *{
        font-family:Helvetica;
    }

    h3{
        text-align: center;
    }

    .contenido-Formulario{
        display: flex;
        align-items: center;
        justify-content: center;
        padding-bottom: 20px;
    }

    input{
        outline-color: crimson;
        padding: 5px;
    }

    input[type="checkbox"]{
        accent-color: crimson;
    }


    input, span{
        margin-left: 5px;
        margin-right: 5px;
    }

    button{
        border: 0;
        background-color: crimson;
        color: white;
        padding: 7px;
        border-radius: 5px;
    }

    .contenedor-Tabla{
        display: flex;
        align-items: center;
        justify-content: center;
    }

    table{
        border: 1px solid black;
        border-collapse: collapse;
    }

    th, td{
        border: 1px solid black;
        padding: 10px;
    }
    
    th{
        background-color: gainsboro;
        text-align: center;
    }
</style>