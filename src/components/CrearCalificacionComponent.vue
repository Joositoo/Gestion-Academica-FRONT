<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { useCalificacionStore } from '../stores/calificacionStore';
import LeftArrowComponent from './LeftArrowComponent.vue';

const calificacionStore = useCalificacionStore();;
const router = useRouter();
let calificaciones = ref(null);

const handleChange = (e) => {
    calificaciones.value = e.target.files[0];
}

const handleSubmit = async () => {
    let pVacio = document.getElementById("vacio");
    let pWrong = document.getElementById("wrongFile");
    let pError500 = document.getElementById("error500");

    if (!calificaciones.value){
        pWrong.style.display = "none";
        pError500.style.display = "none";
        pVacio.style.display = "block";
        return;
    }
    else if (calificaciones.value.type != "text/csv" && !calificaciones.value.name.toLowerCase().endsWith(".csv")){
        pVacio.style.display = "none";
        pError500.style.display = "none";
        pWrong.style.display = "block";
        return;
    }

    try{
        await calificacionStore.saveCalificacion(calificaciones.value);
        router.push("/calificaciones");
    }
    catch{
        pVacio.style.display = "none";
        pWrong.style.display = "none";
        pError500.style.display = "block";
        return;
    }
}

const generateCSV = () => {
    const encabezado = ["nombreModulo", "emailAlumno", "descripcionRa", "nota"];
    const contenidoCSV = encabezado.join(",")+ "\n";

    const blob = new Blob([contenidoCSV], {type: "text/csv;charset=utf-8"});
    const url = URL.createObjectURL(blob);

    const enlace = document.createElement("a");
    enlace.href = url;
    enlace.download = "altaCalificaciones.csv";
    document.body.appendChild(enlace);
    enlace.click();
    document.body.removeChild(enlace);
}
</script>

<template>
    <LeftArrowComponent path="calificaciones" />

    <div class="card-container">
        <div class="card">
            <h2>Registro de calificaciones</h2>

            <div class="flex-container">
                <div>
                    <p>Asegúrate de que el archivo csv contenga la información en este orden: </p>
                    <hr>
                    <img src="/registroCalificaciones.png">
                    <p><button class="crear-editar-input excel" @click="generateCSV">Generar plantilla CSV</button></p>
                </div>
                <div>
                    <form @submit.prevent="handleSubmit">
                        <label for="file"></label>
                        <input type="file" id="file" @change="handleChange">
                        <p><button type="submit" class="crear-editar-input">Registrar</button></p>
                    </form>
                </div>
            </div>
            <p class="error" id="vacio" style="display: none;">Seleccione un archivo, por favor</p>
            <p class="error" id="wrongFile" style="display: none;">El archivo no tiene extensión .csv</p>
            <p class="error" id="error500" style="display: none;">Asegúrate de que el archivo tenga todas las columnas, rellenes todos los datos correctamente, el alumno esté matriculado y no dupliques notas.</p>
        </div>
    </div>
</template>

<style scoped>
.flex-container {
    display: flex;
    flex-direction: row;
    gap: 5em;
}

.flex-container div{
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.error{
    margin-top: 1.22em;
}

form p{
    display: block;
    text-align: center;
    font-size: 1.1em;
}

.excel{
    transition: background-color 0.3s ease;
}

.excel:hover {
    background-color: #17d586;
}
</style>
