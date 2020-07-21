<!--<!doctype html>-->
<!--<html lang="es">-->
<template>
<div>
  <title>Calculadora de Sueldo</title>
  <div>
    <b-navbar fixed="top" toggleable="true" type="dark" variant="dark">
      <b-navbar-brand style="max-width: 550px; margin: auto;" href="#">
        <b-img-lazy rounded="circle" width="40px" fluid src="https://i.imgur.com/KWG4mnv.jpg">
        </b-img-lazy>
        Depto. Educación
      </b-navbar-brand>

      <b-navbar-toggle style="margin-right: auto;" target="nav-collapse" right></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav align="end">
        <b-navbar-nav  align="right">
          <b-nav-item-dropdown text="INSTRUCCIONES" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Ingresa la información que se solicita en el formulario de más abajo.
                Cuando hayas ingresado toda la información correctamente, presiona el botón
                "Calcular Sueldo" y verás el detalle por asignación que deberías recibir
                cada mes, actualizado en la tabla de arriba.
                <br>Puedes cambiar los valores del formulario las veces que quieras, pero luego
                recuerda siempre presionar el botón "Calcular Sueldo" para volver a actualizar
                los datos de la tabla.
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Consideraciones" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Esta calculadora es sólo para uso referencial, ya que, por la forma en
                que realiza los cálculos, es posible que exista una diferencia de
                menos de $5 con el monto real.
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Acerca de" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Esta <b>calculadora de sueldo</b> es fruto del trabajo del <b>Departamento de
                Educación</b> del Comunal Valparaíso del Colegio de Profesoras y Profesores.
                <br>El Departamento, que está integrado por un pequeño grupo de docentes
                de la comuna de Valparaíso, está abierto a la colaboración de cualquier colega
                que tenga interés en participar. Si quieres trabajar con nosotras y
                nosotros, escríbenos al siguiente correo:<br>
              </p>
              <p style="text-align: center;">
                <a style="text-align: center;" href="mailto:depto.educacioncomunal@gmail.com">
                  <b-icon icon="envelope-fill"></b-icon> depto.educacioncomunal@gmail.com
                </a>
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="RRSS" align="end">
            <b-dropdown-item href="https://www.facebook.com/dptoeducacionvalpo/">Facebook</b-dropdown-item>
            <b-dropdown-item href="https://www.instagram.com/dpto.educacion_valparaiso/">Instagram</b-dropdown-item>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Contacto" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Si necesitas contactarte con el Departamento de Educación,
                escríbenos al siguiente correo y te contestaremos a la brevedad:<br>
              </p>
              <p style="text-align: center;">
                <a style="text-align: center;" href="mailto:depto.educacioncomunal@gmail.com">
                  <b-icon icon="envelope-fill"></b-icon> depto.educacioncomunal@gmail.com
                </a>
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item href="https://sites.google.com/view/dptoeducacionvalparaiso" align="end">
            Nuestro sitio web <b-icon icon="box-arrow-up-right"></b-icon>
          </b-nav-item>
          <b-nav-item-dropdown text="Más información" align="end">
            <b-dropdown-item href="https://www.cpeip.cl/valores-2020-brp-y-asignaciones-carrera-docente/">
              <b-icon icon="box-arrow-up-right"></b-icon> Valores 2020 asignaciones
            </b-dropdown-item>
            <b-dropdown-item href="https://github.com/elisa-a-v/sueldoprofesvalpo">
              <b-icon icon="box-arrow-up-right"></b-icon> Repositorio GitHub
            </b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
  <span id="arriba-izq">
    <div style="margin-top: 70px;">
      <h1>
        <br>Calculadora de sueldo
      </h1>
      <p>
        Herramienta para profesoras y profesores que trabajan en
        establecimientos municipales de la comuna de Valparaíso.
        <br><br>
      </p>
    </div>
    <b-container class="body">
      <table id="tabla-colilla"
             class="table table-bordered table-striped table-sm">
        <thead>
          <tr>
            <th style="max-width: 35px;" scope="col">Código</th>
            <th class="d" scope="col">Ítem</th>
            <th style="max-width: 30px;" scope="col">Monto</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in colilla" :key="item">
            <td>{{ item.codigo }}</td>
            <td class="d">{{ item.item }}</td>
            <td>{{ item.monto }}</td>
          </tr>
          <tr>
            <td style="border-right: none;"></td>
            <td class="text-right" style="border-left: none">
              <b>Sueldo bruto:</b>
            </td>
            <td>
              <b>{{ sueldoBruto }}</b>
            </td>
          </tr>
        </tbody>
      </table>
    </b-container>
  </span>
  <span id="abajo-der" style="margin: auto;">
    <h4>
      <br>Formulario
    </h4>
    <table class="table table-hover table-borderless table-striped">
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="fila in filasPosibles" :key="fila">
          <template v-if="(fila.id !== 'horasTotal')
              && !(fila.id === 'prioritario80' && FCS.prioritario60.value !==1)" class="clearfix">
            <span class="clearfix" style="width: 100%;">
              <td style="width: 600px">
                <b-container class="text-left">
                <b-icon icon="info-square-fill" v-b-toggle=fila.tog size="sm"
                        variant="secondary" @click="info(fila.idInfo, fila.info)"></b-icon>
                {{ fila.nombre }}
                <b-form-group>
                    <b-form-select v-if="fila.id === 'valorHora'"
                                :id=fila.id v-model=fila.value>
                      <b-form-select-option v-bind:value="14403">
                        Enseñanza básica
                      </b-form-select-option>
                      <b-form-select-option v-bind:value="15155">
                        Enseñanza media
                      </b-form-select-option>
                    </b-form-select>
                    <b-form-select v-if="fila.id === 'horasRegular'
                    || fila.id === 'horasReemplazo' || fila.id === 'horasSEP'
                    || fila.id === 'horasPIE'" :id=fila.id v-model=fila.value>
                      <b-form-select-option v-for="i in horasPosibles" :key="i" v-bind:value="i">
                        {{ i }}
                      </b-form-select-option>
                    </b-form-select>
                    <b-form-select v-if="fila.id === 'bieniosCormuval'
                    || fila.id === 'bieniosCpeip'"
                    :id=fila.id v-model=fila.value>
                      <b-form-select-option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">
                        {{ i }}
                      </b-form-select-option>
                    </b-form-select>
                    <b-form-select v-if="fila.id === 'tramo'"
                            :id=fila.id v-model=fila.value>
                      <b-form-select-option v-for="i in tramosPosibles" :key="i" v-bind:value="i">
                        {{ i }}
                      </b-form-select-option>
                    </b-form-select>
                    <b-form-select v-if="fila.id === 'nivelBRP'"
                            :id=fila.id v-model=fila.value>
                      <b-form-select-option v-bind:value=0>Sin título</b-form-select-option>
                      <b-form-select-option v-bind:value=253076>
                        Con título, sin mención
                      </b-form-select-option>
                      <b-form-select-option v-bind:value=337436>
                        Con título, con mención
                      </b-form-select-option>
                    </b-form-select>
                    <b-form-select v-if="fila.id === 'prioritario60' || fila.id === 'prioritario80'"
                            :id=fila.id v-model=fila.value>
                      <b-form-select-option v-bind:value=0>No</b-form-select-option>
                      <b-form-select-option v-bind:value=1>Sí</b-form-select-option>
                    </b-form-select>
                  </b-form-group>
                </b-container>
              </td>
            </span>

            <b-collapse :id=fila.tog accordion="info" class="mt-2">
              <b-card>
                <b-card-text class="text-justify">
                  <small :id=fila.idInfo></small>
                </b-card-text>
              </b-card>
            </b-collapse>
            <b-alert show v-if="((fila.value === 'Experto I') ||
            (fila.value === 'Experto II'))
            && FCS.bieniosCpeip.value < 4" variant="danger">
              Revise los datos ingresados.
              Recuerde que para alcanzar el tramo <b>Experto I</b> o
              <b>Experto II</b> no puede tener
              menos de 4 bienios reconocidos por el CPEIP.
            </b-alert>
            <b-alert show v-if="(fila.value === 'Avanzado') && FCS.bieniosCpeip.value < 2"
                     variant="danger">
              Revise los datos ingresados.
              Recuerde que para alcanzar el tramo <B>Avanzado</B>,
              no puede tener menos de 2 bienios reconocidos por el CPEIP.
            </b-alert>

          </template>

          <template v-if="fila.id === 'horasTotal'">
            <span style="margin: auto">
              <td style="margin-left: auto;">
                <b>{{ fila.nombre }}</b>
              </td>
              <td class="d" style="margin-right: auto;">
                <b>{{ horasTotal }}</b>
              </td>
            </span>

            <b-alert show v-if="horasTotal > 44" variant="danger">
              Revise que haya ingresado la cantidad de horas correctamente.
              <br>Recuerde que el máximo legal es de 44 horas semanales.
            </b-alert>
          </template>
        </tr>
      </tbody>
    </table>

    <br>
    <div class="bottom-margin">
      <b-button class="btn btn-success btn-sm" variant="primary" @click="calcularSueldo()">
        Calcular Sueldo
      </b-button>
    </div>
  </span>
</div>
</template>

<script>
// import axios from 'axios';
import Vue from 'vue';
import { BootstrapVue, BootstrapVueIcons, FormPlugin } from 'bootstrap-vue';

Vue.use(BootstrapVue);
Vue.use(BootstrapVueIcons);
Vue.use(FormPlugin);

export default {
  name: 'Home',
  data() {
    return {
      datos: [],
      show: true,
      FCS: {
        valorHora: {
          id: 'valorHora',
          tog: 'valorHoraToggle',
          idInfo: 'valorHoraInfo',
          value: 14403,
          nombre: 'Valor hora:',
          info: 'El valor hora para calcular la Remuneración Básica Mínima Nacional para docentes '
            + 'en Chile depende del nivel en el que se desempeñe la o el docente.'
            + '<br>Para el año 2020 los valores son: '
            + '<br><br><b>Enseñanza básica</b><br>$14.403'
            + '<br><b>Enseñanza media</b><br>$15.155',
        },
        horasRegular: {
          id: 'horasRegular',
          tog: 'horasRegularToggle',
          idInfo: 'horasRegularInfo',
          value: 0,
          nombre: 'Horas por subvención regular:',
          info: 'Cantidad de horas de contrato que son '
            + ' financiadas con la subvención regular;'
            + ' es decir, no son horas SEP, ni de reemplazo, '
            + ' ni PIE, etc.'
            + ' <br>En su liquidación aparece en la parte'
            + ' superior en<br><center>"<b>JORNADA: XX HRS</b>".</center>',
        },
        horasReemplazo: {
          id: 'horasReemplazo',
          tog: 'horasReemplazoToggle',
          idInfo: 'horasReemplazoInfo',
          value: 0,
          nombre: 'Horas de reemplazo:',
          info: 'Horas de reemplazo que realizó durante el mes.',
        },
        horasSEP: {
          id: 'horasSEP',
          tog: 'horasSEPToggle',
          idInfo: 'horasSEPInfo',
          value: 0,
          nombre: 'Horas SEP:',
          info: 'Cantidad de horas financiadas con'
            + ' la Subvención Escolar Preferencial (ley 20.248).',
        },
        horasPIE: {
          id: 'horasPIE',
          tog: 'horasPIEToggle',
          idInfo: 'horasPIEInfo',
          value: 0,
          nombre: 'Horas PIE:',
          info: 'Cantidad de horas financiadas con el Programa de Integración Escolar.',
        },
        horasTotales: {
          value: this.horasTotal,
          id: 'horasTotal',
          tog: '',
          nombre: 'Total de horas:',
          info: '',
          idInfo: '',
        },
        bieniosCormuval: {
          id: 'bieniosCormuval',
          tog: 'bieniosCormuvalToggle',
          idInfo: 'bieniosCormuvalInfo',
          value: 0,
          nombre: 'Bienios CORMUVAL:',
          info: 'Número de bienios (período de 2 años completos) '
            + 'reconocidos por la Corporación Municipal de Valparaíso.',
        },
        bieniosCpeip: {
          id: 'bieniosCpeip',
          tog: 'bieniosCpeipToggle',
          idInfo: 'bieniosCpeipInfo',
          value: 0,
          nombre: 'Bienios CPEIP:',
          info: ' Número de bienios (período de 2 años completos) reconocidos por'
            + ' el Centro de Perfeccionamiento, Experimentación e Investigaciones Pedagógicas.',
        },
        tramo: {
          id: 'tramo',
          tog: 'tramoToggle',
          idInfo: 'tramoInfo',
          value: 'Acceso',
          nombre: 'Tramo Carrera Docente:',
          info: 'Tramo de la Carrera Docente en el que se encuentra.',

        },
        nivelBRP: {
          id: 'nivelBRP',
          tog: 'nivelBRPToggle',
          idInfo: 'nivelBRPInfo',
          value: 0,
          nombre: 'Título para BRP:',
          info: 'El <b>Bono de Reconocimiento Profesional</b>'
            + ' tiene dos niveles, dependiendo'
            + ' de la presencia o ausencia de una "mención" en el título profesional.'
            + ' <br>Los montos para contratos de 30 horas'
            + ' o más, al año 2020 son:'
            + ' <br><br><b>Sin mención</b><br>253.076'
            + ' <br><b>Con mención</b><br>337.436',
        },
        prioritario60: {
          id: 'prioritario60',
          tog: 'prioritario60Toggle',
          idInfo: 'prioritario60Info',
          value: 0,
          nombre: 'Trabaja en un establecimiento con 60% de estudiantes prioritarios o más:',
          info: 'La <b>Asignación por docencia en'
            + ' establecimientos con alta concentración'
            + ' de alumnos prioritarios</b> se paga a'
            + ' todos y todas las docentes que trabajan'
            + ' en establecimientos con un 60%'
            + ' de alumnos prioritarios o más.<br><br>'
            + ' <a href='
            + '"https://www.cpeip.cl/wp-content/uploads/2019/06/Porcentaje-alumnos-prioritarios-2019.pdf">'
            + ' Click aquí'
            + '</a>'
            + ' para ver porcentaje de alumnos'
            + ' prioritarios por establecimiento.',
        },
        prioritario80: {
          id: 'prioritario80',
          tog: 'prioritario80Toggle',
          idInfo: 'prioritario80Info',
          value: 0,
          nombre: 'Trabaja en un establecimiento con 80% de estudiantes prioritarios o más:',
          info: 'La <b>Asignación por docencia en'
            + ' establecimientos con alta concentración de'
            + ' alumnos prioritarios</b> aumenta para docentes en los tramos Avanzado,'
            + ' Experto I y Experto II que trabajen en establecimientos con 80%'
            + ' de estudiantes prioritarios o más.<br><br>'
            + ' <a href='
            + ' "https://www.cpeip.cl/wp-content/uploads/2019/06/Porcentaje-alumnos-prioritarios-2019.pdf">'
            + ' Click aquí'
            + ' </a>'
            + ' para ver porcentaje de alumnos prioritarios por establecimiento.',
        },
      },
      colilla: [
        { codigo: 0, item: 'Sueldo base', monto: 0 },
        { codigo: 8, item: 'Asignación de movilización', monto: 0 },
        { codigo: 25, item: 'Ampliación horaria PIE', monto: 0 },
        { codigo: 32, item: 'Bono Reconocimiento Profesional', monto: 0 },
        { codigo: 47, item: 'Asignación por Desempeño', monto: 0 },
        { codigo: 48, item: 'Ampliación horaria SEP', monto: 0 },
        { codigo: 49, item: 'Ampliación horaria Lic. Med., Reemplazo, etc.', monto: 0 },
        { codigo: 52, item: 'Asignación por Experiencia', monto: 0 },
        { codigo: 80, item: 'Asignación por alta concentración a. prioritarios', monto: 0 },
      ],
      horasPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
        22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44],
      bieniosPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      tramosPosibles: ['Acceso', 'Inicial', 'Temprano', 'Avanzado', 'Experto I', 'Experto II'],
      sueldoBruto: 0,
      horasBRP: 0,
      isHovered: false,
    };
  },
  computed: {
    filasPosibles() {
      return [
        this.FCS.valorHora,
        this.FCS.horasRegular,
        this.FCS.horasReemplazo,
        this.FCS.horasSEP,
        this.FCS.horasPIE,
        this.FCS.horasTotales,
        this.FCS.bieniosCormuval,
        this.FCS.bieniosCpeip,
        this.FCS.tramo,
        this.FCS.nivelBRP,
        this.FCS.prioritario60,
        this.FCS.prioritario80,
      ];
    },
    horasTotal() {
      return this.FCS.horasSEP.value + this.FCS.horasPIE.value
        + this.FCS.horasRegular.value + this.FCS.horasReemplazo.value;
    },
  },
  methods: {
    calcularSueldo() {
      if (this.FCS.prioritario60.value === 0) {
        this.FCS.prioritario80.value = 0;
      }
      const sueldoBase = this.FCS.horasRegular.value * this.FCS.valorHora.value;
      const moviliz = 6921;
      if (this.horasTotal > 30) {
        this.horasBRP = 30;
      } else {
        this.horasBRP = this.horasTotal;
      }
      let BRP = this.horasBRP * this.FCS.nivelBRP.value;
      BRP = Math.round(BRP / 30);
      let asigDesPro1 = this.horasTotal / 44;
      asigDesPro1 *= this.FCS.bieniosCpeip.value / 15;
      let tramoProgresion = 14315;
      let tramoFija = 0;
      if (this.FCS.tramo.value === 'Acceso' || this.FCS.tramo.value === 'Inicial') {
        tramoProgresion = 14315;
      } else if (this.FCS.tramo.value === 'Temprano') {
        tramoProgresion = 47831;
      } else if (this.FCS.tramo.value === 'Avanzado') {
        tramoProgresion = 96266;
        tramoFija = 103410.99;
      } else if (this.FCS.tramo.value === 'Experto I') {
        tramoProgresion = 360892;
        tramoFija = 143625.915;
      } else if (this.FCS.tramo.value === 'Experto II') {
        tramoProgresion = 776654;
        tramoFija = 218311.515;
      }
      asigDesPro1 *= tramoProgresion;
      asigDesPro1 = Math.round(asigDesPro1);
      let asigDesPro2 = this.FCS.bieniosCpeip.value - 1;
      asigDesPro2 *= 0.0333;
      asigDesPro2 += 0.0338;
      asigDesPro2 *= this.horasTotal * this.FCS.valorHora.value;
      asigDesPro2 = Math.round(asigDesPro2);
      let asigDesPro3 = 0;
      asigDesPro3 = this.horasTotal / 44;
      asigDesPro3 *= tramoFija;
      asigDesPro3 = Math.round(asigDesPro3);
      let asigDesPro = 0;
      asigDesPro = asigDesPro1;
      asigDesPro += asigDesPro2;
      asigDesPro += asigDesPro3;
      let amplSEP = this.FCS.bieniosCormuval.value - 1;
      amplSEP *= 0.0333;
      amplSEP += 0.0338;
      amplSEP *= this.FCS.valorHora.value * this.FCS.horasSEP.value;
      amplSEP += (this.FCS.valorHora.value * this.FCS.horasSEP.value);
      amplSEP = Math.round(amplSEP);
      let amplLicOtros = 0.0338 + (0.0333 * (this.FCS.bieniosCormuval.value - 1));
      amplLicOtros *= this.FCS.valorHora.value * this.FCS.horasReemplazo.value;
      amplLicOtros += (this.FCS.valorHora.value * this.FCS.horasReemplazo.value);
      amplLicOtros = Math.round(amplLicOtros);
      let asigExper = sueldoBase * (0.0338 + (0.0333 * (this.FCS.bieniosCormuval.value - 1)));
      asigExper = Math.round(asigExper);
      let asigPrio = (asigDesPro * 0.2) + (65689 * (this.horasTotal / 44));
      let prio = 0;
      if ((this.FCS.tramo.value === 'Avanzado') || (this.FCS.tramo.value === 'Experto I')
        || (this.FCS.tramo.value === 'Experto II')) {
        prio = 1;
      }
      asigPrio *= this.FCS.prioritario80.value * prio;
      asigPrio
        += (this.FCS.prioritario60.value * (asigDesPro * 0.2 + 47872 * (this.horasTotal / 44)));
      asigPrio = Math.round(asigPrio);
      let asigPIE = 0.0338 + (0.0333 * (this.FCS.bieniosCormuval.value - 1));
      asigPIE *= this.FCS.valorHora.value * this.FCS.horasPIE.value;
      asigPIE += (this.FCS.valorHora.value * this.FCS.horasPIE.value);
      asigPIE = Math.round(asigPIE);
      this.colilla[0].monto = sueldoBase;
      this.colilla[1].monto = moviliz;
      this.colilla[2].monto = asigPIE;
      this.colilla[3].monto = BRP;
      this.colilla[4].monto = asigDesPro;
      this.colilla[5].monto = amplSEP;
      this.colilla[6].monto = amplLicOtros;
      this.colilla[7].monto = asigExper;
      this.colilla[8].monto = asigPrio;
      this.sueldoBruto = sueldoBase + moviliz + asigPIE + BRP + asigDesPro + amplSEP
      + amplLicOtros + asigExper + asigPrio;
      window.scrollTo({ top: window, behavior: 'smooth' });
    },
    info(id, inner) {
      document.getElementById(id).innerHTML = inner;
    },
    handleHover(hovered) {
      this.isHovered = hovered;
    },
  },
};

</script>

<style>
div {
  /*max-width: 600px;*/
  margin: auto;
}

span {
  margin: auto;
}

header {
  margin-top: 90px;
  margin-left: 10px;
}

b-card-text {
  text-align: justify !important;
}

.bottom-margin {
  margin-bottom: 20px;
}

.body {
  width: 100%;
}

.d {
  text-align: left;
  max-width: 70px;
}

.i {
  text-align: left;
  max-width: 160px;
}

.clearfix {
  overflow: auto;
  /*content:"";*/
  clear: both;
}

 /* Create three equal columns that floats next to each other */
.column {
  float: left;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

@media screen and (max-width: 600px) {
  .column {
    width: 100%;
  }
}
</style>
<!--</html>-->
