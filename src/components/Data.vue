<!--<!doctype html>-->
<!--<html lang="es">-->
<template>
<span style="max-width: none; justify-content: center;">
  <br>Departamento de Educación - Comunal Valparaíso
  <br>Colegio de Profesoras y Profesores
  <div>
    <h1>
      <br>Calculadora de sueldo
    </h1>
    <h5>
      Herramienta para profesoras y profesores que trabajan en
      establecimientos municipales de la comuna de Valparaíso.
    </h5>

  </div>
  <div>
    <h4>
      <br>INSTRUCCIONES:
    </h4>
    Ingrese la información que se solicita en el formulario a continuación.
    Cuando haya ingresado toda la información correctamente, presione el botón
    "Calcular Sueldo" y verá el detalle por asignación que usted debería recibir
    cada mes.
    <br>Esperamos que esta herramienta le sea de utilidad para revisar su colilla
    de sueldo.
    <br><br>
  </div>
  <div>

    <label>Valor hora:
      <select id="valorHora" v-model="FormCalcularSueldo.valorHora">
        <!-- inline object literal -->
        <option v-bind:value="14403">Enseñanza básica</option>
        <option v-bind:value="15155">Enseñanza media</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Horas por subvención regular:
      <select id="horasRegular" v-model="FormCalcularSueldo.horasRegular">
        <!-- inline object literal -->
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas de reemplazo:
      <select id="horasReemplazo" v-model="FormCalcularSueldo.horasReemplazo">
        <!-- inline object literal -->
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas SEP:
      <select id="horasSEP" v-model="FormCalcularSueldo.horasSEP">
        <!-- inline object literal -->
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas PIE:
      <select id="horasPIE" v-model="FormCalcularSueldo.horasPIE">
        <!-- inline object literal -->
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>
      <b>Horas total contrato:</b> {{ FormCalcularSueldo.horasRegular
      + FormCalcularSueldo.horasReemplazo + FormCalcularSueldo.horasSEP
      + FormCalcularSueldo.horasPIE }}
    </label>
  </div>
  <br>
  <div>
    <label>Bienios reconocidos por CORMUVAL:
      <select id="bieniosCormuval" v-model="FormCalcularSueldo.bieniosCormuval">
        <!-- inline object literal -->
        <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Bienios reconocidos por CPEIP:
      <select id="bieniosCpeip" v-model="FormCalcularSueldo.bieniosCpeip">
        <!-- inline object literal -->
        <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Tramo:
      <select id="tramo" v-model="FormCalcularSueldo.tramo">
        <!-- inline object literal -->
        <option v-for="i in tramosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Título para BRP:
      <select id="nivelBRP" v-model="FormCalcularSueldo.nivelBRP">
        <!-- inline object literal -->
        <option v-bind:value="0">Sin título</option>
        <option v-bind:value="253076">Con título, sin mención</option>
        <option v-bind:value="337436">Con título, con mención</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Trabaja en un establecimiento con 60% de estudiantes prioritarios o más:
      <select id="prioritario60" v-model="FormCalcularSueldo.prioritario60">
        <!-- inline object literal -->
        <option v-bind:value="0">No</option>
        <option v-bind:value="1">Sí</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Trabaja en un establecimiento con 80% de estudiantes prioritarios o más:
      <select id="prioritario80" v-model="FormCalcularSueldo.prioritario80">
        <!-- inline object literal -->
        <option v-bind:value="0">No</option>
        <option v-bind:value="1">Sí</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <button type="button" class="btn btn-success btn-sm"
            @click="calcularSueldo(FormCalcularSueldo)">Calcular Sueldo</button>
    <button type="button" class="btn btn-danger btn-sm" @click="initForm()">
      Limpiar formulario
    </button>
  </div>
  <div id="detalle-calculado">
  </div>
</span>
</template>

<script>
// import axios from 'axios';

export default {
  name: 'Home',
  data() {
    return {
      datos: [],
      FormCalcularSueldo: {
        valorHora: 0,
        horasRegular: 0,
        horasReemplazo: 0,
        horasSEP: 0,
        horasPIE: 0,
        horasTotal: 0,
        bieniosCormuval: 0,
        bieniosCpeip: 0,
        tramo: '',
        tramoProgresion: 0,
        tramoFija: 0,
        nivelBRP: 0,
        horasBRP: 0,
        prioritario60: 0,
        prioritario80: 0,
        avanzadoExperto: 0,
      },
      horasPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
        22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44],
      bieniosPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      tramosPosibles: ['Acceso', 'Inicial', 'Temprano', 'Avanzado', 'Experto I', 'Experto II'],
    };
  },
  methods: {
    initForm() {
      let i;
      const variables = ['valorHora', 'horasRegular', 'horasReemplazo', 'horasSEP', 'horasPIE',
        'bieniosCormuval', 'bieniosCpeip', 'tramo', 'nivelBRP',
        'horasBRP', 'prioritario60', 'prioritario80'];
      for (i = 0; i < 14; i += 1) {
        const el = document.getElementById(variables[i]);
        if (variables[i] === 'tramo') {
          el.value = '';
        } else {
          el.value = 0;
        }
        el.dispatchEvent((new Event('select')));
      }
    },
    calcularSueldo(payload) {
      alert(payload.toString());
      this.initForm();
    },
  },
};
</script>

<style>
div {
  max-width: 800px;
  margin: auto;
}
</style>
<!--</html>-->
