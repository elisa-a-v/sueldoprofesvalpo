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
      <br><br>
    </h5>
  </div>
  <div>
    <table class="table table-hover table-bordered table-striped table-sm">
      <thead>
        <tr>
          <th scope="col">Código</th>
          <th scope="col">Ítem</th>
          <th scope="col">Monto</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in colilla" :key="item">
          <td>{{ item.codigo }}</td>
          <td>{{ item.item }}</td>
          <td>{{ item.monto }}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <div>
    <h4>
      <br>INSTRUCCIONES:
    </h4>
    Ingrese la información que se solicita en el formulario a continuación.
    Cuando haya ingresado toda la información correctamente, presione el botón
    "Calcular Sueldo" y verá el detalle por asignación que usted debería recibir
    cada mes en la tabla de arriba.
    <br><br>Esperamos que esta herramienta le sea de utilidad para revisar su colilla
    de sueldo.
    <br><br>
  </div>
  <div>
    <label>Valor hora:
      <select id="valorHora" v-model="FCS.valorHora">
        <option v-bind:value="14403">Enseñanza básica</option>
        <option v-bind:value="15155">Enseñanza media</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Horas por subvención regular:
      <select id="horasRegular" v-model="FCS.horasRegular">
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas de reemplazo:
      <select id="horasReemplazo" v-model="FCS.horasReemplazo">
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas SEP:
      <select id="horasSEP" v-model="FCS.horasSEP">
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Horas PIE:
      <select id="horasPIE" v-model="FCS.horasPIE">
        <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>
      <b>Horas total contrato:</b> {{ FCS.horasPIE + FCS.horasReemplazo + FCS.horasRegular
      + FCS.horasSEP }}
    </label>
  </div>
  <br>
  <div>
    <label>Bienios reconocidos por CORMUVAL:
      <select id="bieniosCormuval" v-model="FCS.bieniosCormuval">
        <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Bienios reconocidos por CPEIP:
      <select id="bieniosCpeip" v-model="FCS.bieniosCpeip">
        <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <div>
    <label>Tramo:
      <select id="tramo" v-model="FCS.tramo">
        <option v-for="i in tramosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Título para BRP:
      <select id="nivelBRP" v-model="FCS.nivelBRP">
        <option v-bind:value="0">Sin título</option>
        <option v-bind:value="253076">Con título, sin mención</option>
        <option v-bind:value="337436">Con título, con mención</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Trabaja en un establecimiento con 60% de estudiantes prioritarios o más:
      <select id="prioritario60" v-model="FCS.prioritario60">
        <option v-bind:value="0">No</option>
        <option v-bind:value="1">Sí</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <label>Trabaja en un establecimiento con 80% de estudiantes prioritarios o más:
      <select id="prioritario80" v-model="FCS.prioritario80">
        <option v-bind:value="0">No</option>
        <option v-bind:value="1">Sí</option>
      </select>
    </label>
  </div>
  <br>
  <div>
    <b-button class="btn btn-success btn-sm" variant="primary" @click="calcularSueldo()">
      Calcular Sueldo
    </b-button>
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
      FCS: {
        valorHora: 0,
        horasRegular: 0,
        horasReemplazo: 0,
        horasSEP: 0,
        horasPIE: 0,
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
      colilla: [
        { codigo: 0, item: 'Sueldo base', monto: 0 },
        { codigo: 8, item: 'Asignación de movilización', monto: 0 },
        { codigo: 25, item: 'Ampliación horaria PIE', monto: 0 },
        { codigo: 32, item: 'Bono Reconocimiento Profesional', monto: 0 },
        { codigo: 47, item: 'Asignación por Desempeño', monto: 0 },
        { codigo: 48, item: 'Ampliación horaria SEP', monto: 0 },
        { codigo: 49, item: 'Ampliación horaria Lic. Med.', monto: 0 },
        { codigo: 52, item: 'Asignación por Experiencia', monto: 0 },
        { codigo: 80, item: 'Asignación Prioritario', monto: 0 },
        { codigo: '-', item: 'SUELDO BRUTO', monto: 0 },
      ],
      horasPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
        22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44],
      bieniosPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      tramosPosibles: ['Acceso', 'Inicial', 'Temprano', 'Avanzado', 'Experto I', 'Experto II'],
      horasTotal: 0,
    };
  },
  methods: {
    calcularSueldo() {
      const sueldoBase = this.FCS.horasRegular * this.FCS.valorHora;
      const moviliz = 6921;
      this.horasTotal = this.FCS.horasSEP + this.FCS.horasReemplazo + this.FCS.horasPIE
      + this.FCS.horasRegular;
      if (this.horasTotal > 30) {
        this.FCS.horasBRP = 30;
      } else {
        this.FCS.horasBRP = this.horasTotal;
      }
      let BRP = this.FCS.horasBRP * this.FCS.nivelBRP;
      BRP = Math.round(BRP / 30);
      let asigDesPro1 = this.horasTotal / 44;
      asigDesPro1 *= this.FCS.bieniosCpeip / 15;
      let tramoProgresion = 0;
      let tramoFija = 0;
      if (this.FCS.tramo === 'Acceso' && this.FCS.tramo === 'Inicial') {
        tramoProgresion = 14315;
      } else if (this.FCS.tramo === 'Temprano') {
        tramoProgresion = 47831;
      } else if (this.FCS.tramo === 'Avanzado') {
        tramoProgresion = 96266;
        tramoFija = 103410.99;
      } else if (this.FCS.tramo === 'Experto I') {
        tramoProgresion = 360892;
        tramoFija = 143625.915;
      } else if (this.FCS.tramo === 'Experto II') {
        tramoProgresion = 776654;
        tramoFija = 218311.515;
      }
      asigDesPro1 *= tramoProgresion;
      asigDesPro1 = Math.round(asigDesPro1);
      let asigDesPro2 = this.FCS.bieniosCpeip - 1;
      asigDesPro2 *= 0.0333;
      asigDesPro2 += 0.0338;
      asigDesPro2 *= this.horasTotal * this.FCS.valorHora;
      asigDesPro2 = Math.round(asigDesPro2);
      let asigDesPro3 = 0;
      asigDesPro3 = this.horasTotal / 44;
      asigDesPro3 *= tramoFija;
      asigDesPro3 = Math.round(asigDesPro3);
      let asigDesPro = 0;
      asigDesPro = asigDesPro1;
      asigDesPro += asigDesPro2;
      asigDesPro += asigDesPro3;
      let amplSEP = this.FCS.bieniosCormuval - 1;
      amplSEP *= 0.0333;
      amplSEP += 0.0338;
      amplSEP *= this.FCS.valorHora * this.FCS.horasSEP;
      amplSEP += (this.FCS.valorHora * this.FCS.horasSEP);
      amplSEP = Math.round(amplSEP);
      const amplLicOtros = 0;
      const asigExper = 0;
      const asigPrio = 0;
      const asigPIE = 0;
      this.colilla[0].monto = sueldoBase;
      this.colilla[1].monto = moviliz;
      this.colilla[2].monto = asigPIE;
      this.colilla[3].monto = BRP;
      this.colilla[4].monto = asigDesPro;
      this.colilla[5].monto = amplSEP;
      this.colilla[6].monto = amplLicOtros;
      this.colilla[7].monto = asigExper;
      this.colilla[8].monto = asigPrio;
      this.colilla[9].monto = sueldoBase + moviliz + asigPIE + BRP + asigDesPro + amplSEP
      + amplLicOtros + asigExper + asigPrio;
    },
  },
};
</script>

<style>
div {
  max-width: 600px;
  margin: auto;
}
</style>
<!--</html>-->
