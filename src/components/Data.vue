<!--<!doctype html>-->
<!--<html lang="es">-->
<template>
<span>
  <div style="width: content-box">
    <b-navbar fixed="top" toggleable="true" type="dark" variant="dark">
      <b-navbar-brand href="#">
        <b-img-lazy rounded="circle" width="50px" fluid src="https://i.imgur.com/KWG4mnv.jpg">
        </b-img-lazy>
        Depto. Educación
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse" right></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav align="end">
        <b-navbar-nav  align="right">
          <b-nav-item-dropdown text="Instrucciones" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Ingrese la información que se solicita en el formulario a continuación.
                Cuando haya ingresado toda la información
                correctamente, presione el botón
                "Calcular Sueldo" y verá el detalle por asignación que usted debería recibir
                cada mes, actualizado en la tabla de arriba.
                <br>Puede cambiar los valores del formulario las veces que quiera, pero luego
                recuerde siempre presionar el botón "Calcular Sueldo" para volver a actualizar
                los datos de la tabla.
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Advertencia" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                El uso de esta calculadora es sólo a modo referencial, ya que debido a la forma en
                que esta aplicación realiza los cálculos, es posible que exista una diferencia de
                menos de $10 con el monto real.
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item-dropdown text="Acerca de" align="end">
            <b-dropdown-text>
              <p style="text-align: justify; overflow-wrap: break-word;
              word-wrap: break-word; word-break-wrap: break-word; margin: 10px;">
                Esta <b>calculadora de sueldo</b> es producto del trabajo del Departamento de
                Educación del Comunal Valparaíso del Colegio de Profesoras y Profesores.
                <br>El Departamento, que está integrado por un grupo de docentes en ejercicio
                de la comuna de Valparaíso, está abierto a la colaboración de cualquier persona
                del gremio que tenga interés en participar. Si quieres trabajar con nosotras y
                nosotros, escríbenos al siguiente correo:<br>
              </p>
              <p style="text-align: center;">
                <a style="text-align: center;" href="mailto:depto.educacioncomunal@gmail.com">
                  depto.educacioncomunal@gmail.com
                </a>
              </p>
            </b-dropdown-text>
          </b-nav-item-dropdown>
          <b-nav-item href="https://sites.google.com/view/dptoeducacionvalparaiso" align="end">
            Nuestro sitio web
          </b-nav-item>
          <b-nav-item-dropdown text="RRSS" align="end">
            <b-dropdown-item href="https://www.facebook.com/dptoeducacionvalpo/">Facebook</b-dropdown-item>
            <b-dropdown-item href="https://www.instagram.com/dpto.educacion_valparaiso/">Instagram</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
  <b-container id="arriba-izq">
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
             class="table table-bordered table-striped table-sm table-responsive-sm">
        <thead>
          <tr>
            <th scope="col">Código</th>
            <th class="d" scope="col">Ítem</th>
            <th scope="col">Monto</th>
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
            <td class="i" style="border-left: none">
              <b>Sueldo bruto:</b>
            </td>
            <td>
              <b>{{ sueldoBruto }}</b>
            </td>
          </tr>
        </tbody>
      </table>
    </b-container>
  </b-container>
  <b-container id="abajo-der">
    <h4>
      <br>Formulario
    </h4>
    <table class="table table-hover table-borderless table-striped">
      <tbody>
        <tr>
          <td class="i">
            Valor hora:
            <div>
             <b-button v-b-toggle.collapse-1 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-1" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    El valor hora para calcular la Remuneración Básica Mínima Nacional para
                    docentes en Chile depende del nivel en el que se desempeñe la o el docente.
                    Para el año 2020 los valores son:
                    <br>Enseñanza básica: $14.403
                    <br>Enseñanza media: $15.155
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="valorHora" v-model="FCS.valorHora">
              <option v-bind:value="14403">Enseñanza básica</option>
              <option v-bind:value="15155">Enseñanza media</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Horas por subvención regular:
            <div>
             <b-button v-b-toggle.collapse-2 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-2" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Cantidad de horas de contrato que son financiadas con la subvención regular;
                    es decir, no son horas SEP, ni de reemplazo, ni PIE, etc.
                    <br>En su liquidación aparece en la parte superior en "JORNADA: XX HRS".
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="horasRegular" v-model="FCS.horasRegular">
              <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Horas de reemplazo:
            <div>
             <b-button v-b-toggle.collapse-3 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-3" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Horas de reemplazo que realizó durante el mes.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="horasReemplazo" v-model="FCS.horasReemplazo">
              <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Horas SEP:
            <div>
             <b-button v-b-toggle.collapse-4 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-4" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Cantidad de horas financiadas con la Subvención Escolar Preferencial
                    (ley 20.248).
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="horasSEP" v-model="FCS.horasSEP">
              <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Horas PIE:
            <div>
             <b-button v-b-toggle.collapse-5 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-5" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Cantidad de horas financiadas con el Programa de Integración Escolar.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="horasPIE" v-model="FCS.horasPIE">
              <option v-for="i in horasPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td v-if="(FCS.horasPIE + FCS.horasReemplazo + FCS.horasRegular
            + FCS.horasSEP) < 45" class="i">
            <b>Horas total contrato:</b>
          </td>
          <td v-else class="i" style="color: red;">
            <b>Horas total contrato:</b>
            <b-alert show variant="danger">
              Revise que haya ingresado la cantidad de horas correctamente. Recuerde que
              el máximo legal es de 44 horas semanales.
            </b-alert>
          </td>
          <td v-if="(FCS.horasPIE + FCS.horasReemplazo + FCS.horasRegular
            + FCS.horasSEP) < 45" class="d">
            {{ FCS.horasPIE + FCS.horasReemplazo + FCS.horasRegular
            + FCS.horasSEP }}
          </td>
          <td v-else class="d" style="color: red;">
            {{ FCS.horasPIE + FCS.horasReemplazo + FCS.horasRegular
            + FCS.horasSEP }}
          </td>
        </tr>
        <tr>
          <td class="i">
            Bienios reconocidos por CORMUVAL:
            <div>
             <b-button v-b-toggle.collapse-6 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-6" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Número de bienios (período de 2 años completos) reconocidos por
                    la Corporación Municipal de Valparaíso.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
              <select id="bieniosCormuval" v-model="FCS.bieniosCormuval">
                <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
              </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Bienios reconocidos por CPEIP:
            <div>
             <b-button v-b-toggle.collapse-7 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-7" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Número de bienios (período de 2 años completos) reconocidos por
                    el Centro de Perfeccionamiento, Experimentación e Investigaciones Pedagógicas.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="bieniosCpeip" v-model="FCS.bieniosCpeip">
              <option v-for="i in bieniosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Tramo:
            <div>
             <b-button v-b-toggle.collapse-8 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-8" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    Tramo de la Carrera Profesional Docente en el que se encuentra.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
            <b-alert show v-if="((FCS.tramo === 'Experto I') ||
            (FCS.tramo === 'Experto II')) && FCS.bieniosCpeip < 4" variant="danger">
              Revise los datos ingresados. Recuerde que para alcanzar el tramo <b>Experto I</b> o
              <b>Experto II</b> no puede tener menos de 4 bienios reconocidos por el CPEIP.
            </b-alert>
            <b-alert show v-if="(FCS.tramo === 'Avanzado') && FCS.bieniosCpeip < 2"
                     variant="danger">
              Revise los datos ingresados. Recuerde que para alcanzar el tramo <B>Avanzado</B>,
              no puede tener menos de 2 bienios reconocidos por el CPEIP.
            </b-alert>
          </td>
          <td class="d">
            <select id="tramo" v-model="FCS.tramo">
              <option v-for="i in tramosPosibles" :key="i" v-bind:value="i">{{ i }}</option>
            </select>
          </td>
        </tr>
        <tr>
          <td class="i">
            Título para BRP:
            <div>
             <b-button v-b-toggle.collapse-9 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-9" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    El Bono de Reconocimiento Profesional se otorga a profesionales titulados o
                    tituladas, y tiene dos niveles. Para el año 2020 los montos son los siguientes:
                    <br>Sólo título, sin mención: $253.076
                    <br>Título y mención: $337.436
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="nivelBRP" v-model="FCS.nivelBRP">
              <option v-bind:value="0">Sin título</option>
              <option v-bind:value="253076">Con título, sin mención</option>
              <option v-bind:value="337436">Con título, con mención</option>
            </select>
            <br>
          </td>
        </tr>
        <tr>
          <td class="i">
            Trabaja en un establecimiento con 60% de estudiantes prioritarios o más:
            <div>
             <b-button v-b-toggle.collapse-10 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-10" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    La <b>Asignación por docencia en establecimientos con alta concentración de
                    alumnos prioritarios</b> se paga a todos y todas las docentes que trabajan
                    en establecimientos con un 60% de alumnos prioritarios o más.<br>
                    <a href=
       "https://www.cpeip.cl/wp-content/uploads/2019/06/Porcentaje-alumnos-prioritarios-2019.pdf">
                      Click aquí
                    </a>
                     para ver porcentaje de alumnos prioritarios por establecimiento.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="prioritario60" v-model="FCS.prioritario60">
              <option v-bind:value="0">No</option>
              <option v-bind:value="1">Sí</option>
            </select>
          </td>
        </tr>
        <tr v-if="FCS.prioritario60 === 1">
          <td class="i">
            Trabaja en un establecimiento con 80% de estudiantes prioritarios o más:
            <div>
             <b-button v-b-toggle.collapse-11 pill size="sm" variant="secondary">?</b-button>
              <b-collapse id="collapse-11" class="mt-2">
                <b-card
                  style="max-width: 20rem;"
                  align="left"
                >
                  <b-card-text>
                    La <b>Asignación por docencia en establecimientos con alta concentración de
                    alumnos prioritarios</b> aumenta para docentes en los tramos Avanzado,
                    Experto I y Experto II que trabajen en establecimientos con 80%
                    de estudiantes prioritarios o más.<br>
                    <a href=
       "https://www.cpeip.cl/wp-content/uploads/2019/06/Porcentaje-alumnos-prioritarios-2019.pdf">
                      Click aquí
                    </a>
                     para ver porcentaje de alumnos prioritarios por establecimiento.
                  </b-card-text>
                </b-card>
              </b-collapse>
            </div>
          </td>
          <td class="d">
            <select id="prioritario80" v-model="FCS.prioritario80">
              <option v-bind:value="0">No</option>
              <option v-bind:value="1">Sí</option>
            </select>
          </td>
        </tr>
      </tbody>
    </table>
    <br>
    <div class="bottom-margin">
      <b-button class="btn btn-success btn-sm" variant="primary" @click="calcularSueldo()">
        Calcular Sueldo
      </b-button>
    </div>
  </b-container>
</span>
</template>

<script>
// import axios from 'axios';
import Vue from 'vue';
import { BootstrapVue } from 'bootstrap-vue';

Vue.use(BootstrapVue);

export default {
  name: 'Home',
  data() {
    return {
      datos: [],
      show: true,
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
        { codigo: 49, item: 'Ampliación horaria Lic. Med., Reemplazo, etc.', monto: 0 },
        { codigo: 52, item: 'Asignación por Experiencia', monto: 0 },
        { codigo: 80, item: 'Asignación por alta concentración a. prioritarios', monto: 0 },
      ],
      horasPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
        22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44],
      bieniosPosibles: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      tramosPosibles: ['Acceso', 'Inicial', 'Temprano', 'Avanzado', 'Experto I', 'Experto II'],
      horasTotal: 0,
      sueldoBruto: 0,
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
      let tramoProgresion = 14315;
      let tramoFija = 0;
      if (this.FCS.tramo === 'Acceso' || this.FCS.tramo === 'Inicial') {
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
      let amplLicOtros = 0.0338 + (0.0333 * (this.FCS.bieniosCormuval - 1));
      amplLicOtros *= this.FCS.valorHora * this.FCS.horasReemplazo;
      amplLicOtros += (this.FCS.valorHora * this.FCS.horasReemplazo);
      amplLicOtros = Math.round(amplLicOtros);
      let asigExper = sueldoBase * (0.0338 + (0.0333 * (this.FCS.bieniosCormuval - 1)));
      asigExper = Math.round(asigExper);
      let asigPrio = (asigDesPro * 0.2) + (65689 * (this.horasTotal / 44));
      let prio = 0;
      if ((this.FCS.tramo === 'Avanzado') || (this.FCS.tramo === 'Experto I')
        || (this.FCS.tramo === 'Experto II')) {
        prio = 1;
      }
      asigPrio *= this.FCS.prioritario80 * prio;
      asigPrio += (this.FCS.prioritario60 * (asigDesPro * 0.2 + 47872 * (this.horasTotal / 44)));
      asigPrio = Math.round(asigPrio);
      let asigPIE = this.FCS.valorHora * (0.0338 + (0.0333 * (this.FCS.bieniosCormuval - 1)));
      asigPIE *= this.FCS.horasPIE;
      asigPIE += (this.FCS.valorHora * this.FCS.horasPIE);
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
  },
};

</script>

<style>
div {
  max-width: 600px;
  margin: auto;
}

span {
  margin: auto;
}

select {
  max-width: 90px;
}

header {
  margin-top: 90px;
  margin-left: 10px;
}

.bottom-margin {
  margin-bottom: 20px;
}

.body {
  width: 100%;
}

.d {
  text-align: left;
}

.i {
  text-align: right;
  max-width: 160px;
}
</style>
<!--</html>-->
