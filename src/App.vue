<template>
  <v-app id="app">
    <v-container fluid style="height: 100vh" class="background">
      <!-- <h1 style="color: yellow;">QUIMIPEDIA</h1> -->
      <v-img src="./assets/qm.png" max-height="100px" max-width="200px"></v-img>
      <categories :groups="groups" @change="changeCategory"></categories>
      <br />
      <v-row class="background">
        <v-container fluid style="width: 100%">
          <v-layout>
            <v-row>
              <v-col md="9" style="width: 100%">
                <v-row
                  wrap
                  no-gutters
                  v-for="(row, rindex) in qelements"
                  :key="rindex"
                  style="min-width: 100%"
                >
                  <v-col v-for="(col, cindex) in row" :key="cindex" class="box">
                    <v-tooltip right open-delay="400">
                      <template v-slot:activator="{ on, attrs }">
                        <v-hover v-if="col.dibujar" v-slot="{ hover }">
                          <div class="bordeado" style="height: 100%">
                            <v-card
                              dark
                              tile
                              flat
                              :color="hover ? 'orange' : getColor(col)"
                              :elevation="hover ? 12 : 0"
                              v-bind="attrs"
                              v-on="on"
                              outlined
                              style="height: 100%"
                            >
                              <v-card-text class="pa-0" style="width: 100%">
                                <div class="el-num-atom text-no-wrap">
                                  {{ col.num_atomico }}
                                </div>
                                <div class="el-simbolo text-no-wrap">
                                  {{ col.simbolo }}
                                </div>
                                <!-- <div class="el-nombre text-no-wrap"> -->
                                <div
                                  style="
                                    font-size: 0.63vw;
                                    color: black;
                                    text-align: center;
                                    margin: 0 auto;
                                  "
                                  class="text-no-wrap"
                                >
                                  {{ col.nombre }}
                                </div>
                              </v-card-text>
                            </v-card>
                          </div>
                        </v-hover>
                      </template>
                      <v-card max-width="600" min-width="500" flat>
                        <v-card-text style="text-align: center">
                          <h1>{{ col.nombre }}</h1>
                        </v-card-text>
                        <v-row>
                          <v-col>
                            <v-row>
                              <v-col>
                                <v-img
                                  v-if="col.src"
                                  height="250"
                                  width="250"
                                  :src="
                                    require('./assets/' + col.simbolo + '.jpg')
                                  "
                                >
                                  <v-col>
                                    <div
                                      style="
                                        background-color: white;
                                        opacity: 60%;
                                      "
                                    >
                                      <v-row
                                        style="color: black; font-size: x-large"
                                        class="v-card-content"
                                      >
                                        <b
                                          style="
                                            color: black;
                                            font-size: x-large;
                                          "
                                          >{{ col.num_atomico }}</b
                                        >
                                      </v-row>
                                      <v-row class="v-card-content">
                                        <b
                                          style="
                                            color: black;
                                            font-size: x-large;
                                          "
                                          >{{ col.simbolo }}</b
                                        >
                                      </v-row>
                                    </div>
                                  </v-col>
                                </v-img>
                              </v-col>
                            </v-row>
                            <v-row> </v-row>
                          </v-col>
                          <v-col style="color: black">
                            <div class="description">
                              <div><b>Nombre Común:</b> {{ col.nombre }}</div>
                              <div>
                                <b>Serie Química:</b> {{ col.serie_quimica }}
                              </div>
                              <div>
                                <b>Estado Natural:</b> {{ col.estado_natural }}
                              </div>
                              <div><b>Color:</b> {{ col.color_info }}</div>
                              <div>
                                <b>Numero atómico:</b> {{ col.num_atomico }}
                              </div>
                              <div><b>Grupo:</b> {{ col.grupo }}</div>
                              <div><b>Dureza:</b> {{ col.dureza }}</div>
                              <div>
                                <b>Masa atómica:</b> {{ col.masa_atomica }}
                              </div>
                              <div>
                                <b>Ubicación en el Mundo:</b>
                                {{ col.ubicacion_mundial }}
                              </div>
                              <div>
                                <b>Tipo de Explotación:</b>
                                {{ col.tipo_exploracion }}
                              </div>
                              <div><b>Demanda:</b> {{ col.demanda }}</div>
                              <div><b>Utilidad:</b> {{ col.utilidad }}</div>
                              <div>
                                <b>Electronegatividad:</b>
                                {{ col.electronegatividad }}
                              </div>
                              <div>
                                <b>Estado de Oxidación:</b>
                                {{ col.estado_de_oxidacion }}
                              </div>
                              <div>
                                <b>Minerales Asociados:</b>
                                {{ col.minerales_asoc }}
                              </div>
                            </div>
                          </v-col>
                        </v-row>
                        <v-row align="center">
                          <v-col>
                            <div class="description move-right"></div>
                          </v-col>
                          <v-col> </v-col>
                        </v-row>
                      </v-card>
                    </v-tooltip>
                  </v-col>
                </v-row>
              </v-col>
              <v-col md="3" style="width: 100%">
                <questions></questions>
              </v-col>
            </v-row>
          </v-layout>
          <v-container fluid style="width: 100%">
            <v-layout>
              <v-col md="9" style="width: 100%">
                <v-row 
                  wrap
                  no-gutters
                  v-for="(row, idx) in extra_elements" 
                  :key="idx"
                  style="min-width: 100%;">
                  <v-col v-for="(col, cidx) in row" :key="cidx">
                    <v-tooltip right open-delay="400">
                      <template v-slot:activator="{ on, attrs }">
                        <v-hover v-if="col.dibujar" v-slot="{ hover }">
                          <div class="bordeado" style="height: 100%">
                            <v-card
                              dark
                              tile
                              flat
                              :color="hover ? 'orange' : getColor(col)"
                              :elevation="hover ? 12 : 0"
                              v-bind="attrs"
                              v-on="on"
                              outlined
                              style="height: 100%"
                            >
                              <v-card-text class="pa-0" style="width: 100%">
                                <div class="el-num-atom text-no-wrap">
                                  {{ col.num_atomico }}
                                </div>
                                <div class="el-simbolo text-no-wrap">
                                  {{ col.simbolo }}
                                </div>
                                <!-- <div class="el-nombre text-no-wrap"> -->
                                <div
                                  style="
                                    font-size: 0.63vw;
                                    color: black;
                                    text-align: center;
                                    margin: 0 auto;
                                  "
                                  class="text-no-wrap"
                                >
                                  {{ col.nombre }}
                                </div>
                              </v-card-text>
                            </v-card>
                          </div>
                        </v-hover>
                      </template>
                      <v-card max-width="600" min-width="500" flat>
                        <v-card-text style="text-align: center">
                          <h1>{{ col.nombre }}</h1>
                        </v-card-text>
                        <v-row>
                          <v-col>
                            <v-row>
                              <v-col>
                                <v-img
                                  v-if="col.src"
                                  height="250"
                                  width="250"
                                  :src="
                                    require('./assets/' + col.simbolo + '.jpg')
                                  "
                                >
                                  <v-col>
                                    <div
                                      style="
                                        background-color: white;
                                        opacity: 60%;
                                      "
                                    >
                                      <v-row
                                        style="color: black; font-size: x-large"
                                        class="v-card-content"
                                      >
                                        <b
                                          style="
                                            color: black;
                                            font-size: x-large;
                                          "
                                          >{{ col.num_atomico }}</b
                                        >
                                      </v-row>
                                      <v-row class="v-card-content">
                                        <b
                                          style="
                                            color: black;
                                            font-size: x-large;
                                          "
                                          >{{ col.simbolo }}</b
                                        >
                                      </v-row>
                                    </div>
                                  </v-col>
                                </v-img>
                              </v-col>
                            </v-row>
                            <v-row> </v-row>
                          </v-col>
                          <v-col style="color: black">
                            <div class="description">
                              <div><b>Nombre Común:</b> {{ col.nombre }}</div>
                              <div>
                                <b>Serie Química:</b> {{ col.serie_quimica }}
                              </div>
                              <div>
                                <b>Estado Natural:</b> {{ col.estado_natural }}
                              </div>
                              <div><b>Color:</b> {{ col.color_info }}</div>
                              <div>
                                <b>Numero atómico:</b> {{ col.num_atomico }}
                              </div>
                              <div><b>Grupo:</b> {{ col.grupo }}</div>
                              <div><b>Dureza:</b> {{ col.dureza }}</div>
                              <div>
                                <b>Masa atómica:</b> {{ col.masa_atomica }}
                              </div>
                              <div>
                                <b>Ubicación en el Mundo:</b>
                                {{ col.ubicacion_mundial }}
                              </div>
                              <div>
                                <b>Tipo de Explotación:</b>
                                {{ col.tipo_exploracion }}
                              </div>
                              <div><b>Demanda:</b> {{ col.demanda }}</div>
                              <div><b>Utilidad:</b> {{ col.utilidad }}</div>
                              <div>
                                <b>Electronegatividad:</b>
                                {{ col.electronegatividad }}
                              </div>
                              <div>
                                <b>Estado de Oxidación:</b>
                                {{ col.estado_de_oxidacion }}
                              </div>
                              <div>
                                <b>Minerales Asociados:</b>
                                {{ col.minerales_asoc }}
                              </div>
                            </div>
                          </v-col>
                        </v-row>
                        <v-row align="center">
                          <v-col>
                            <div class="description move-right"></div>
                          </v-col>
                          <v-col> </v-col>
                        </v-row>
                      </v-card>
                    </v-tooltip>
                  </v-col>
                </v-row>
              </v-col>
            </v-layout>
          </v-container>
        </v-container>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import Questions from "./components/Questions.vue";
import Categories from "./components/Categories.vue";
export default {
  components: {
    Questions,
    Categories,
  },
  name: "App",
  data: () => ({
    selectedColor: "red",
    unselectedColor: "grey",
    selectedCategory: null,
    qelements: [
      [
        {
          simbolo: "H",
          nombre: "Hidrogeno",
          num_atomico: 1,
          masa_atomica: 1.0,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/H.jpg",
          serie_quimica: "No Metales",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "1",
          dureza: "N/A",
          electronegatividad: "2.2",
          estado_de_oxidacion: "-1, 1, 0",
          minerales_asoc: "N/A",
          ubicacion_mundial: "Atmósfera de todo el planeta",
          tipo_exploracion: "N/A",
          demanda: "Muy Alta",
          utilidad:
            "Industria petroquímica, agente hidrogenizante en grasas y aceites, elemento de soldadura, detector de fugas, sustituto de combustibles fósiles.",
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          simbolo: "He",
          nombre: "Helio",
          num_atomico: 2,
          masa_atomica: 4.0,
          dibujar: true,
          tags: ["Gases Nobles"],
          estado: "Gaseoso",
          color: "purple",
          src: "./assets/He.jpg",
          serie_quimica: "No Metales",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "2",
          dureza: "N/A",
          electronegatividad: "N/A",
          estado_de_oxidacion: "0",
          minerales_asoc:
            "Uranio, torio, cleveíta, pechbenda, carnotita, monacita",
          ubicacion_mundial:
            "Atmósfera de todo el planeta, Estados Unidos, Rusia, Polonia, Qatar, Tanzania",
          tipo_exploracion: "Desintegración radioactiva",
          demanda: "Alta",
          utilidad:
            "Inmersiones a gran profundidad, cromatografía de gases, elemento de soldadura, agente refrigerante, uso en globos, dirigibles y combustible de cohetes espaciales.",
        },
      ],
      [
        {
          simbolo: "Li",
          nombre: "Litio",
          num_atomico: 3,
          masa_atomica: 6.9,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
          src: "./assets/Li.jpg",
          serie_quimica: "Metal alcalino",
          estado_natural: "Sólido",
          color_info: "Plateado",
          grupo: "1",
          dureza: "0.6",
          electronegatividad: "1",
          estado_de_oxidacion: "1",
          minerales_asoc:
            "Lepidolita, petalita, espodumena (foto), ambligolita ",
          ubicacion_mundial:
            "Argentina, Bolivia, Chile, Perú, Colombia, Estados Unidos",
          tipo_exploracion: "Cielo Abierto",
          demanda: "Alta – Muy Alta",
          utilidad:
            "Baterías recargables y no recargables, secantes en bombas de calor, lubricantes de alta temperatura, aleaciones para construcciones aeronáuticas, estabilizador del estado del ánimo.",
        },
        {
          simbolo: "Be",
          nombre: "Berilio",
          num_atomico: 4,
          masa_atomica: 9.0,
          dibujar: true,
          tags: ["Alcalinotérreos"],
          color: "amber",
          src: "./assets/Li.jpg",
          serie_quimica: "Metal alcalinotérreo",
          estado_natural: "Sólido",
          color_info: "Gris metálico, blanco grisáceo",
          grupo: "1",
          dureza: "5.5",
          electronegatividad: "1.57",
          estado_de_oxidacion: "2",
          minerales_asoc: "Berilo (foto), bertrandita, crisoberilo, fenaquita ",
          ubicacion_mundial:
            "Austria, Alemania, Irlanda, Madagascar, Rusia Brasil, Sudáfrica, China",
          tipo_exploracion: "Subterránea",
          demanda: "Alta",
          utilidad:
            "Aleaciones, conductores de calor y electricidad, litografía de rayos X, industria petrolera y nuclear, instrumentos de precisión.",
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          simbolo: "B",
          nombre: "Boro",
          num_atomico: 5,
          masa_atomica: 10.8,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
          src: "./assets/B.jpg",
          serie_quimica: "Semimetal, metaloide",
          estado_natural: "Sólido",
          color_info: "Marrón, negro.",
          grupo: "5",
          dureza: "9.5",
          electronegatividad: "2.04",
          estado_de_oxidacion: "3",
          minerales_asoc:
            "Depósitos evaporíticos (bórax) (foto), sasolitas, pegmatitas ",
          ubicacion_mundial:
            "Estados Unidos, Argentina, Turquía, Italia, Chile",
          tipo_exploracion: "Cielo Abierto",
          demanda: "Alta",
          utilidad:
            "Aplicaciones mecánicas especiales, fuegos pirotécnicos, productos textiles, agente semiconductor, conservante de la madera, alternativa de combustible.",
        },
        {
          simbolo: "C",
          nombre: "Carbono",
          num_atomico: 6,
          masa_atomica: 12.0,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/C.jpg",
          serie_quimica: "No metal",
          estado_natural: "Sólido",
          color_info: "Opaco (grafito) – transparente (diamante)",
          grupo: "6",
          dureza: "1 (grafito) – 10 (diamante)",
          electronegatividad: "2.55",
          estado_de_oxidacion: "4, 2",
          minerales_asoc:
            "Caliza, dolomita, mármol, kimberlita (foto), lamproita ",
          ubicacion_mundial:
            "Rusia, Estados Unidos, México, Groenlandia, Sudáfrica, Namibia, Rep. Del Congo, Brasil, Australia",
          tipo_exploracion: "Cielo Abierto – Subterráneo",
          demanda: "Muy Alta",
          utilidad:
            "Componente de hidrocarburos, fabricación de lápices, aditivo de lubricantes, joyería, varas de protección nucleares, medicina, filtración y purificación del agua",
        },
        {
          simbolo: "N",
          nombre: "Nitrogeno",
          num_atomico: 7,
          masa_atomica: 14.0,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/N.jpg",
          serie_quimica: "No metal",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "7",
          dureza: "N/A",
          electronegatividad: "3.04",
          estado_de_oxidacion: "+/- 3, 1, 2, 4, 5",
          minerales_asoc:
            "Caliza (foto), calcita, dolomía, yeso, alabastro, feldespatos ",
          ubicacion_mundial: "Atmósfera de todo el planeta",
          tipo_exploracion: "N/A",
          demanda: "Alta – Muy Alta",
          utilidad:
            "Elemento del aire, Obtención del amoníaco, fertilizantes, fabricación de pólvora y nitroglicerina, combustible de cohetes, gas criogénico",
        },
        {
          simbolo: "O",
          nombre: "Oxigeno",
          num_atomico: 8,
          masa_atomica: 15.9,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/O.jpg",
          serie_quimica: "No metal",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "8",
          dureza: "N/A",
          electronegatividad: "3.44",
          estado_de_oxidacion: "-2",
          minerales_asoc:
            "Wustita, sílices, bauxita, corindón, hematita, caliza",
          ubicacion_mundial: "Aire, tierra y agua del planeta",
          tipo_exploracion: "N/A",
          demanda: "Muy Alta",
          utilidad:
            "Indispensable para vida humana, insuficiencias cardíacas, medicina hiperbárica, ventilación mecánica, trajes espaciales, fundición del acero, anticongelantes, determinar indicios de vida en otros planetas.",
        },
        {
          simbolo: "F",
          nombre: "Fluor",
          num_atomico: 9,
          masa_atomica: 19.0,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
          src: "./assets/F.jpg",
          serie_quimica: "Halógeno",
          estado_natural: "Gaseoso",
          color_info: "Gris pálido, verde – amarillo",
          grupo: "9",
          dureza: "N/A",
          electronegatividad: "3.98",
          estado_de_oxidacion: "-1",
          minerales_asoc: "Fluorita, fluorapatito, criolita (foto)",
          ubicacion_mundial:
            "China, México, Mongolia, Sudáfrica, España, Rusia",
          tipo_exploracion: "Subterránea",
          demanda: "Media – Alta",
          utilidad:
            "Teflón, CFC, enriquecimiento de uranio, compuestos con pasta de dientes, semiconductores.",
        },
        {
          simbolo: "Ne",
          nombre: "Neon",
          num_atomico: 10,
          masa_atomica: 20.2,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
          src: "./assets/Ne.jpg",
          serie_quimica: "Gas noble",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "10",
          dureza: "N/A",
          electronegatividad: "N/A",
          estado_de_oxidacion: "0",
          minerales_asoc: "N/A",
          ubicacion_mundial: "Atmósfera de todo el planeta",
          tipo_exploracion: "N/A",
          demanda: "Alta",
          utilidad:
            "Indicadores de alto voltaje, tubos de televisión, refrigerante criogénico.",
        },
      ],
      [
        {
          simbolo: "Na",
          nombre: "Sodio",
          num_atomico: 11,
          masa_atomica: 25.0,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
          src: "./assets/Na.jpg",
          serie_quimica: "Metal alcalino",
          estado_natural: "Sólido",
          color_info: "Plateado",
          grupo: "11",
          dureza: "1.2",
          electronegatividad: "0.93",
          estado_de_oxidacion: "1",
          minerales_asoc: "Amarillita, jadeita, halita (foto), zeolita",
          ubicacion_mundial: "Agua salada de todo el planeta",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Formación de sal, limpieza de desagües, aleaciones antifricción, desodorantes, purificación de metales, transferencia de calor, iluminación.",
        },
        {
          simbolo: "Mg",
          nombre: "Magnesio",
          num_atomico: 12,
          masa_atomica: 24.3,
          dibujar: true,
          tags: ["Alcalinotérreos"],
          color: "amber",
          src: "./assets/Mg.jpg",
          serie_quimica: "Metal alcalinotérreo",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "12",
          dureza: "2.5",
          electronegatividad: "1.31",
          estado_de_oxidacion: "2",
          minerales_asoc:
            "Dolomita, magnesita (foto), dolomía, brucita, carnalita, olivino",
          ubicacion_mundial:
            "Brasil, India, Austria, Polonia, Rusia, China, Estados Unidos",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Material refractario, elemento de aleación con aluminio, aditivo en propelentes, agente reductor de uranio, mejora de agarre de objetos.",
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          simbolo: "Al",
          nombre: "Aluminio",
          num_atomico: 13,
          masa_atomica: 27.0,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
          src: "./assets/Al.jpg",
          serie_quimica: "Metal del bloque p",
          estado_natural: "Sólido",
          color_info: "Gris claro",
          grupo: "13",
          dureza: "2.80",
          electronegatividad: "1.61",
          estado_de_oxidacion: "2, 8, 3",
          minerales_asoc: "Bauxita, gibbsita, boehmita, diásporo",
          ubicacion_mundial:
            "Caribe, Australia, Brasil, África, Vietnam, Grecia, Irán, Venezuela",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Uso industrial, espejos domésticos e industriales, papel aluminio, aeronáutica, contenedores criogénicos.",
        },
        {
          simbolo: "Si",
          nombre: "Silicio",
          num_atomico: 14,
          masa_atomica: 18.1,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
          src: "./assets/Si.jpg",
          serie_quimica: "Semimetal, metaloide",
          estado_natural: "Sólido",
          color_info: "Gris oscuro",
          grupo: "14",
          dureza: "7",
          electronegatividad: "1.9",
          estado_de_oxidacion: "4",
          minerales_asoc:
            "Arena, cuarzo, amatista, ágata, jaspe, ópalo, granito (foto), feldespato, arcilla, hornblenda",
          ubicacion_mundial: "Casi en todo el planeta",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Aleaciones en cerámica, industria electrónica y microelectrónica, fabricación de hormigón y ladrillos, elemento fertilizante, fabricación de vidrio, implantes de seno y lentes de contacto.",
        },
        {
          simbolo: "P",
          nombre: "Fosforo",
          num_atomico: 15,
          masa_atomica: 30.97,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/P.jpg",
          serie_quimica: "No metal",
          estado_natural: "Sólido",
          color_info: "Incoloro, rojo plateado",
          grupo: "15",
          dureza: "5",
          electronegatividad: "2.19",
          estado_de_oxidacion: "+/- 3, 5",
          minerales_asoc: "Apatita (foto)",
          ubicacion_mundial:
            "Marruecos, Rusia, Estados Unidos, Sahara Occidental, España, Perú",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Alimentos y bebidas, agricultura e hidroponía, acuarios de agua salada, calderas de refrigeración, purificación de agua.",
        },
        {
          simbolo: "S",
          nombre: "Azufre",
          num_atomico: 16,
          masa_atomica: 30.97,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/S.jpg",
          serie_quimica: "No metal",
          estado_natural: "Sólido",
          color_info: "Amarillo limón",
          grupo: "16",
          dureza: "2",
          electronegatividad: "2.58",
          estado_de_oxidacion: "+/- 2, 4, 6",
          minerales_asoc:
            "Pirita (foto), galena, yeso, cinabrio, esfalerita, estibina, combustibles fósiles",
          ubicacion_mundial:
            "Estados Unidos, Australia, Suiza, República Checa, Suecia, Noruega, Rusia, Japón",
          tipo_exploracion: "Cielo abierto y subterránea",
          demanda: "Alta",
          utilidad:
            "Producción de baterías, fabricación de pólvora, vulcanizado de caucho, blanqueamiento de papel, fijador en fotografías, antiséptico, fungicida.",
        },
        {
          simbolo: "Cl",
          nombre: "Cloro",
          num_atomico: 17,
          masa_atomica: 35.453,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
          src: "./assets/Cl.jpg",
          serie_quimica: "Halógeno",
          estado_natural: "Gaseoso",
          color_info: "Amarillo verdoso",
          grupo: "17",
          dureza: "N/A",
          electronegatividad: "3.16",
          estado_de_oxidacion: "+/- 1, 3, 5, 7",
          minerales_asoc: "Carnalita (foto)",
          ubicacion_mundial: "China",
          tipo_exploracion: "N/A",
          demanda: "Alta",
          utilidad:
            "Catalizador, industria alimentaria, metalúrgica, productos de limpieza, abrillantador de pisos, desinfectante, industria de explosivos, CFC, pesticidas.",
        },
        {
          simbolo: "Ar",
          nombre: "Argon",
          num_atomico: 18,
          masa_atomica: 39.948,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
          src: "./assets/Ar.jpg",
          serie_quimica: "Gas noble",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "18",
          dureza: "N/A",
          electronegatividad: "N/A",
          estado_de_oxidacion: "0",
          minerales_asoc: "N/A",
          ubicacion_mundial: "Atmósfera de todo el planeta",
          tipo_exploracion: "N/A",
          demanda: "Media",
          utilidad:
            "Lámparas incandescentes, soldadura de arco, fabricación de titanio y monocristales, datación de núcleos de hielo, inflado de trajes secos, láser de odontología.",
        },
      ],
      [
        {
          simbolo: "K",
          nombre: "Potasio",
          num_atomico: 19,
          masa_atomica: 39.0983,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
          src: "./assets/K.jpg",
          serie_quimica: "Metal alcalino",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "19",
          dureza: "0.5",
          electronegatividad: "0.82",
          estado_de_oxidacion: "1",
          minerales_asoc: "Carnalita, langbeinita, polihalita, silvina (foto)",
          ubicacion_mundial: "España, Alemania, Italia, Estados Unidos",
          tipo_exploracion: "Cielo abierto",
          demanda: "Media – Alta",
          utilidad:
            "Células fotoeléctricas, fertilizantes, fabricación de pólvora, fabricación de cristales, formación de sales, elemento básico en alimentación humana.",
        },
        {
          simbolo: "Ca",
          nombre: "Calcio",
          num_atomico: 20,
          masa_atomica: 40.078,
          dibujar: true,
          tags: ["Alcalinotérreos", "En Ecuador"],
          color: "amber",
          src: "./assets/Ca.jpg",
          serie_quimica: "Metal alcalinotérreo",
          estado_natural: "Sólido",
          color_info: "Gris suave, blanco plateado",
          grupo: "2",
          dureza: "1.75",
          electronegatividad: "1",
          estado_de_oxidacion: "2",
          minerales_asoc:
            "Caliza (foto), calcita, dolomía, yeso, alabastro, feldespatos ",
          ubicacion_mundial:
            "México, Brasil, Alemania, Japón, Estados Unidos, China, Reino Unido",
          tipo_exploracion: "Cielo Abierto",
          demanda: "Alta – Muy Alta",
          utilidad:
            "Desoxidante para metales, coagulación de la leche, cemento para construcción, insecticidas, creación de cal y sulfato de calcio.",
        },
        {
          simbolo: "Sc",
          nombre: "Escandio",
          num_atomico: 21,
          masa_atomica: 44.95591,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sc.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "3",
          dureza: "7.5",
          electronegatividad: "1.36",
          estado_de_oxidacion: "3",
          minerales_asoc: "Euxenita, galodinita, thortveitita (foto)",
          ubicacion_mundial: "Zona de Escandinavia, Madagascar",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Lámparas de luz solar artificial, aleación con titanio, industria aeroespacial.",
        },
        {
          simbolo: "Ti",
          nombre: "Titanio",
          num_atomico: 22,
          masa_atomica: 47.867,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Ti.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco metálico",
          grupo: "4",
          dureza: "6",
          electronegatividad: "1.54",
          estado_de_oxidacion: "-1, 1, 2, 3, 4",
          minerales_asoc:
            "Anatasa, brookita, ilmenita, perovskita, rutilo, titanita (foto)",
          ubicacion_mundial:
            "Australia, Canadá, China, India, Mozambique, Nueva Zelanda, Noruega, Ucrania, Sudáfrica, Kazajistán",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Desoxidante, reducción del carbono, pigmentos y aditivos, alta resistencia a corrosión, intercambiadores de calor, aleaciones en autos, joyería, herramientas quirúrgicas.",
        },
        {
          simbolo: "V",
          nombre: "Vanadio",
          num_atomico: 23,
          masa_atomica: 50.9415,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/V.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco grisáceo",
          grupo: "5",
          dureza: "7.0",
          electronegatividad: "1.63",
          estado_de_oxidacion: "2, 3, 4, 5",
          minerales_asoc: "Patronita, vanadinita (foto), carnotita",
          ubicacion_mundial: "Sudáfrica, China, Rusia",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Aditivo de aceros, instrumentos quirúrgicos, estabilizador en llantas, componentes de reactores nucleares, imanes superconductores, cerámica, aleaciones de acero.",
        },
        {
          simbolo: "Cr",
          nombre: "Cromo",
          num_atomico: 24,
          masa_atomica: 51.9962,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/V.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Plateado metálico",
          grupo: "6",
          dureza: "8.5",
          electronegatividad: "1.66",
          estado_de_oxidacion: "2, 3, 6",
          minerales_asoc: "Cromita (foto)",
          ubicacion_mundial: "Sudáfrica, Kazajistán, India, Turquía, Rusia",
          tipo_exploracion: "Cielo abierto",
          demanda: "Muy Alta",
          utilidad:
            "Resistencia a la corrosión en metalurgia, aleación de acero inoxidable, pinturas y colorantes, limpieza de vidrios de laboratorio, catalizadores, materiales refractarios, preservación de la madera.",
        },
        {
          simbolo: "Mn",
          nombre: "Magnesio",
          num_atomico: 25,
          masa_atomica: 54.93804,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Mn.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco grisáceo",
          grupo: "6",
          dureza: "8.5",
          electronegatividad: "1.66",
          estado_de_oxidacion: "2, 3, 6",
          minerales_asoc: "Cromita (foto)",
          ubicacion_mundial: "Sudáfrica, Kazajistán, India, Turquía, Rusia",
          tipo_exploracion: "Cielo abierto",
          demanda: "Muy Alta",
          utilidad:
            "Resistencia a la corrosión en metalurgia, aleación de acero inoxidable, pinturas y colorantes, limpieza de vidrios de laboratorio, catalizadores, materiales refractarios, preservación de la madera.",
        },
        {
          simbolo: "Fe",
          nombre: "Hierro",
          num_atomico: 26,
          masa_atomica: 55.85,
          dibujar: true,
          tags: ["Metales Transitorios", "En Ecuador"],
          color: "pink",
          src: "./assets/Fe.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Blanco",
          grupo: "8",
          dureza: "5.5",
          electronegatividad: "1.83",
          estado_de_oxidacion: "2, 3",
          minerales_asoc:
            "Hematita (foto), magnetita, ilmenita, limonita, siderita, pirita.",
          ubicacion_mundial:
            "Australia, Brasil, Rusia, China, Ucrania, Canadá, India, Estados Unidos.",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Siderurgia, aleaciones como el hierro forjado, hierro colado, acero; aplicaciones médicas, industria automotriz, aeronáutica, naval y construcción.",
        },
        {
          simbolo: "Co",
          nombre: "Cobalto",
          num_atomico: 27,
          masa_atomica: 58.93319,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco azulado",
          grupo: "9",
          dureza: "4",
          electronegatividad: "1.88",
          estado_de_oxidacion: "-1, 1, 2, 3, 4, 5",
          minerales_asoc: "Cobaltitas, carrolita, linneita (foto)",
          ubicacion_mundial: "Estados Unidos, Alemania, Suecia ",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Superaleaciones para turbinas de gas, aleaciones para corrosión, imanes, secante para pinturas y barnices, pigmentos, electrodos de baterías eléctricas, cables de acero de neumáticos.",
        },
        {
          simbolo: "Ni",
          nombre: "Niquel",
          num_atomico: 28,
          masa_atomica: 58.6934,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Ni.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Blanco con tono amarillo",
          grupo: "10",
          dureza: "5",
          electronegatividad: "1.91",
          estado_de_oxidacion: "0, 2, 3",
          minerales_asoc:
            "Kamacita, taenita, garnierita (foto), millerita, pentladita, pirrotina, niquelina.",
          ubicacion_mundial:
            "Indonesia, Filipinas, Nueva Caledonia, Rusia, Australia, Canadá, China, Cuba, Brasil.",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Fabricación de acero inoxidable, alnico para imanes, aleaciones para motores marinos, usos en robótica, crisoles de laboratorios clínicos, acuñación de monedas, creación de oro blanco.",
        },
        {
          simbolo: "Cu",
          nombre: "Cobre",
          num_atomico: 29,
          masa_atomica: 63.546,
          dibujar: true,
          tags: ["Metales Transitorios", "En Ecuador"],
          color: "pink",
          src: "./assets/Cu.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Pardo rojizo medio",
          grupo: "11",
          dureza: "3",
          electronegatividad: "1.9",
          estado_de_oxidacion: "+1, +3",
          minerales_asoc:
            "Cobre nativo (foto), Cuprita, Covelina, Calcopirita, Pirita, Calcosina, Bornita",
          ubicacion_mundial:
            "Chile, Mongolia, Indonesia, México, Perú, Brasil, Estados Unidos",
          tipo_exploracion: "Cielo Abierto y Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Alambres eléctricos, circuitos, partes y repuestos automotrices, acuñación de monedas, ornamentación, industria de construcción, obtención de aleaciones como latón y bronce.",
        },
        {
          simbolo: "Zn",
          nombre: "Zinc",
          num_atomico: 30,
          masa_atomica: 65.38,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Zn.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Blanco azulado",
          grupo: "12",
          dureza: "2.5",
          electronegatividad: "1.6",
          estado_de_oxidacion: "2",
          minerales_asoc:
            "Esfalerita (foto), smithsonita, hemimorfita, franklinita.",
          ubicacion_mundial:
            "China, Perú, Australia, India, Estados Unidos, Canadá, México, Bolivia, Irlanda.",
          tipo_exploracion: "Cielo abierto, subterráneo",
          demanda: "Alta",
          utilidad:
            "Baterías de uso espacial y para laptops, piezas de fundición para automoción, eliminación de la plata del plomo, fabricación de pinturas de óleo, galvanización y fabricación de láminas de construcción.",
        },
        {
          simbolo: "Ga",
          nombre: "Galio",
          num_atomico: 31,
          masa_atomica: 69.723,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
          src: "./assets/Ga.jpg",
          serie_quimica: "Metal del bloque p",
          estado_natural: "Sólido",
          color_info: "Grisáceo",
          grupo: "13",
          dureza: "1.5",
          electronegatividad: "1.81",
          estado_de_oxidacion: "3",
          minerales_asoc:
            "Bauxita, carbón, diásporo (foto), germanita, esfalerita.",
          ubicacion_mundial:
            "Rusia, Eslovaquia, Suiza, Grecia, Argentina, Chile, Perú.",
          tipo_exploracion: "Cielo abierto",
          demanda: "Alta",
          utilidad:
            "Semiconductores, circuitos de microondas, diodos LED, armas nucleares, paneles solares, producción de espejos, termómetros médicos.",
        },
        {
          simbolo: "Ge",
          nombre: "Germanio",
          num_atomico: 32,
          masa_atomica: 72.64,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
          src: "./assets/Ge.jpg",
          serie_quimica: "Semimetal, metaloide",
          estado_natural: "Sólido",
          color_info: "Blanco grisáceo",
          grupo: "14",
          dureza: "6",
          electronegatividad: "2.01",
          estado_de_oxidacion: "-4, -3, -2, -1, 0, 1, 2, 3, 4",
          minerales_asoc: "Germanita (foto), garnierita, carbón, argidorita.",
          ubicacion_mundial: "Rusia, China.",
          tipo_exploracion: "Cielo abierto",
          demanda: "Baja – Media",
          utilidad:
            "Fibras ópticas, radares y amplificadores de guitarras eléctricas, óptica de infrarrojos, lentes de alta refracción, joyería, quimioterapia.",
        },
        {
          simbolo: "As",
          nombre: "Arsenico",
          num_atomico: 33,
          masa_atomica: 74.9216,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
          src: "./assets/As.jpg",
          serie_quimica: "Semimetal, metaloide",
          estado_natural: "Sólido",
          color_info: "Gris metálico",
          grupo: "15",
          dureza: "3.5",
          electronegatividad: "2.0",
          estado_de_oxidacion: "3, 5",
          minerales_asoc: "Arsenopirita (foto)",
          ubicacion_mundial: "China, Perú, Filipinas, Chile, Canadá",
          tipo_exploracion: "Subterráneo",
          demanda: "Media – Alta",
          utilidad:
            "Elemento esencial para la vida, preservante de madera, semiconductor en circuitos integrados, aditivo en aleaciones de plomo, insecticida, pigmento para pirotecnia, decolorante de vidrios.",
        },
        {
          simbolo: "Se",
          nombre: "Selenio",
          num_atomico: 34,
          masa_atomica: 78.96,
          dibujar: true,
          tags: ["Otros no metales"],
          color: "green",
          src: "./assets/Se.jpg",
          serie_quimica: "No metal",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "16",
          dureza: "2",
          electronegatividad: "2.48",
          estado_de_oxidacion: "-2, 2, 4, 6",
          minerales_asoc: "Rocas y suelo de toda la tierra",
          ubicacion_mundial: "Alrededor del planeta",
          tipo_exploracion: "Cielo abierto",
          demanda: "Baja – Media",
          utilidad: "Fabricación de vidrio, tratamiento para la dermatitis.",
        },
        {
          simbolo: "Br",
          nombre: "Bromo",
          num_atomico: 35,
          masa_atomica: 79.904,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
          src: "./assets/Br.jpg",
          serie_quimica: "Halógeno",
          estado_natural: "Líquido",
          color_info: "Blanco plateado",
          grupo: "17",
          dureza: "N/A",
          electronegatividad: "2.96",
          estado_de_oxidacion: "+/- 1, 3, 5, 7",
          minerales_asoc: "Agua de mar",
          ubicacion_mundial: "Estados Unidos, Israel",
          tipo_exploracion: "N/A",
          demanda: "Baja",
          utilidad:
            "Aplicaciones químicas e industriales, sedantes, placas fotográficas.",
        },
        {
          simbolo: "Kr",
          nombre: "Kripton",
          num_atomico: 36,
          masa_atomica: 83.798,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
          src: "./assets/Kr.jpg",
          serie_quimica: "Gas noble",
          estado_natural: "Gaseoso",
          color_info: "Incoloro",
          grupo: "18",
          dureza: "N/A",
          electronegatividad: "3.00",
          estado_de_oxidacion: "0",
          minerales_asoc: "N/A",
          ubicacion_mundial: "Atmósfera del planeta",
          tipo_exploracion: "N/A",
          demanda: "Media",
          utilidad:
            "Anestesia (alto riesgo), fotografía, lámparas de flash, proyectores de alta definición, fabricación de circuitos.",
        },
      ],
      [
        {
          simbolo: "Rb",
          nombre: "Rubidio",
          num_atomico: 37,
          masa_atomica: 85.4678,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
          src: "./assets/Rb.jpg",
          serie_quimica: "Metal alcalino",
          estado_natural: "Sólido",
          color_info: "Plateado blanquecino",
          grupo: "1",
          dureza: "0.3",
          electronegatividad: "0.82",
          estado_de_oxidacion: "1",
          minerales_asoc: "Leucita, polucita, zinwaldita, lepidolita (foto)",
          ubicacion_mundial: "Superficie de todo el planeta",
          tipo_exploracion: "Cielo abierto, subterránea",
          demanda: "Media",
          utilidad:
            "Motores iónicos para naves espaciales, recubrimientos fotoemisores, componente de fotorresistencias, tomografías de emisión de positrones, turbinas de vapor.",
        },
        {
          simbolo: "Sr",
          nombre: "Estronico",
          num_atomico: 38,
          masa_atomica: 87.62,
          dibujar: true,
          tags: ["Alcalinotérreos"],
          color: "amber",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal alcalinotérreo",
          estado_natural: "Sólido",
          color_info: "Plateado brillante",
          grupo: "2",
          dureza: "1.5",
          electronegatividad: "0.95",
          estado_de_oxidacion: "2",
          minerales_asoc: "Celestina, estroncianita, estroncita",
          ubicacion_mundial:
            "China, España, México, Turquía, Argentina, Irán, Inglaterra",
          tipo_exploracion: "Cielo abierto",
          demanda: "Media",
          utilidad:
            "Pirotecnia, imanes, refinamiento del zinc, producción de vidrios, cerámicas, pigmentos para pinturas, terapia para el cáncer, tratamiento de osteoporosis.",
        },
        {
          simbolo: "Y",
          nombre: "Itrio",
          num_atomico: 39,
          masa_atomica: 88.90585,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "3",
          dureza: "5",
          electronegatividad: "1.22",
          estado_de_oxidacion: "2",
          minerales_asoc: "Gadolinita",
          ubicacion_mundial: "Noruega, Suecia, Estados Unidos",
          tipo_exploracion: "Cielo abierto",
          demanda: "Media",
          utilidad:
            "Refrigerante en motores de aviones, recubrimiento en turbinas de gas, electro cerámica, producción de células de combustible, joyería, cuchillos no metálicos.",
        },
        {
          simbolo: "Zr",
          nombre: "Zirconio",
          num_atomico: 40,
          masa_atomica: 91.224,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Plateado brillante",
          grupo: "4",
          dureza: "3",
          electronegatividad: "1.33",
          estado_de_oxidacion: "4",
          minerales_asoc: "Rocas silíceas, granito, circón",
          ubicacion_mundial: "Australia, Brasil, India, Rusia, Estados Unidos",
          tipo_exploracion: "Cielo abierto y Subterráneo",
          demanda: "Media – Alta",
          utilidad:
            "Reactores nucleares, aditivo de aceros, aleaciones con níquel, crisoles de laboratorio, intercambiadores de calor, elementos superconductores, joyería, arenas sintéticas.",
        },
        {
          simbolo: "Nb",
          nombre: "Niobio",
          num_atomico: 41,
          masa_atomica: 92.90638,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Gris metálico",
          grupo: "5",
          dureza: "6",
          electronegatividad: "1.6",
          estado_de_oxidacion: "5",
          minerales_asoc: "Columbita (foto), euxenita, samarskita, fergunosita",
          ubicacion_mundial: "Brasil",
          tipo_exploracion: "Cielo abierto y Subterráneo",
          demanda: "Media",
          utilidad:
            "Componente de acero inoxidable, aleación con titanio para imanes superconductores, lentes y pantallas de cristal, lámparas de vapor de sodio, joyería, fabricación de monedas bimetálicas.",
        },
        {
          simbolo: "Mo",
          nombre: "Molibdeno",
          num_atomico: 42,
          masa_atomica: 95.96,
          dibujar: true,
          tags: ["Metales Transitorios", "En Ecuador"],
          color: "pink",
          src: "./assets/Mo.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "6",
          dureza: "5.5",
          electronegatividad: "2.16",
          estado_de_oxidacion: "2, 3, 4, 5, 6",
          minerales_asoc:
            "Molibdenita (foto), Molibdita, Powellita, Ferrimolibdita",
          ubicacion_mundial: "Estados Unidos, China, Chile, Perú, Canadá",
          tipo_exploracion:
            "Cielo Abierto y Subterránea (subproducto de minería de cobre)",
          demanda: "Alta",
          utilidad:
            "Industria petrolera, tintes plásticos, construcción de autos y aviones, aplicaciones electrónicas, pinturas y lubricantes.",
        },
        {
          simbolo: "Tc",
          nombre: "Tecnecio",
          num_atomico: 43,
          masa_atomica: 98,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Gris plateado",
          grupo: "7",
          dureza: "N/A",
          electronegatividad: "1.9",
          estado_de_oxidacion: "1, 3, 4, 5, 6, 7",
          minerales_asoc: "N/A",
          ubicacion_mundial: "N/A",
          tipo_exploracion: "N/A",
          demanda: "Baja",
          utilidad:
            "Medicina nuclear, aplicaciones industriales, catalizador, protección para hierros y aceros para corrosión.",
        },
        {
          simbolo: "Ru",
          nombre: "Rutenio",
          num_atomico: 44,
          masa_atomica: 101.07,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco grisáceo",
          grupo: "8",
          dureza: "6.5",
          electronegatividad: "2.2",
          estado_de_oxidacion: "2",
          minerales_asoc: "Laurita, anduorita, platarsita, pentladita (foto)",
          ubicacion_mundial: "Región de los Montes Urales",
          tipo_exploracion: "Cielo abierto",
          demanda: "Media",
          utilidad:
            "Aleaciones para endurecer platino y paladio, aleación para titanio, catalizador en refinería petroleras.",
        },
        {
          simbolo: "Rh",
          nombre: "Rodio",
          num_atomico: 45,
          masa_atomica: 102.9055,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "6",
          dureza: "6.0",
          electronegatividad: "2.28",
          estado_de_oxidacion: "1, 2, ,3, 4, 5, 6",
          minerales_asoc: "Rhodita, boweita",
          ubicacion_mundial: "Sudáfrica, Rusia",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Galvanizar oro blanco, catalizador para hidrogenación e hidrocarburnos, contactos eléctricos.",
        },
        {
          simbolo: "Pd",
          nombre: "Paladio",
          num_atomico: 46,
          masa_atomica: 106.42,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "10",
          dureza: "4.75",
          electronegatividad: "2.20",
          estado_de_oxidacion: "1, 2, 4, 6",
          minerales_asoc:
            "Estibiopaladinita, naldreiita, polarita, potarita (foto)",
          ubicacion_mundial:
            "Rusia, Australia, Etiopía, Sudáfrica y América del Norte",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Joyería, odontología, relojería, condensadores eléctricos.",
        },
        {
          simbolo: "Ag",
          nombre: "Plata",
          num_atomico: 47,
          masa_atomica: 107.8682,
          dibujar: true,
          tags: ["Metales Transitorios", "En Ecuador"],
          color: "pink",
          src: "./assets/Ag.jpg",
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado o gris claro",
          grupo: "11",
          dureza: "2.5 – 3",
          electronegatividad: "1.93",
          estado_de_oxidacion: "+1, +2, +3, +4",
          minerales_asoc:
            "Plata nativa con cuarzo (foto), Calcita, Cobre, Arsénico, Calcosina, Galena",
          ubicacion_mundial:
            "México, Rep. Checa, Alemania, España, Australia, China",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Mejor conductor de la electricidad, ornamentación, joyería, aparatos y circuitos eléctricos, fines medicinales, antisépticos.",
        },
        {
          simbolo: "Cd",
          nombre: "Cadmio",
          num_atomico: 48,
          masa_atomica: 112.441,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal de transición",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "12",
          dureza: "2",
          electronegatividad: "1.69",
          estado_de_oxidacion: "1, 2",
          minerales_asoc: "Greenockita (foto)",
          ubicacion_mundial:
            "Rusia, Australia, Etiopía, Sudáfrica y América del Norte",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Acumuladores eléctricos, barras de control de neutrones en reactores, fabricación de esmaltes, galvanotecnia, fotografía y tintorería.",
        },
        {
          simbolo: "In",
          nombre: "Indio",
          num_atomico: 49,
          masa_atomica: 114.818,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal del bloque p",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "13",
          dureza: "1.2",
          electronegatividad: "1.78",
          estado_de_oxidacion: "3",
          minerales_asoc:
            "Abramovita, minerales de tierras raras, roquesita (foto)",
          ubicacion_mundial: "Japón, China",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Motores de alto rendimiento, pantallas de cristal líquido (LED), fotoconductores, paneles electro luminiscentes, medicina nuclear.",
        },
        {
          simbolo: "Sn",
          nombre: "Estano",
          num_atomico: 50,
          masa_atomica: 118.71,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
          src: "./assets/Sr.jpg",
          serie_quimica: "Metal del bloque p",
          estado_natural: "Sólido",
          color_info: "Blanco plateado",
          grupo: "14",
          dureza: "1.5",
          electronegatividad: "1.96",
          estado_de_oxidacion: "2, 4",
          minerales_asoc: "Casiterita (foto)",
          ubicacion_mundial:
            "Alemania, Francia, Portugal, España, Brasil, Bolivia, Indonesia, China",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Protector del hierro para latas de conserva, fungicidas, tintes, dentífricos, pigmentos, uso en etiquetas, material de soldadura, esmaltes cerámicos, sobre taponado de botellas de vino.",
        },
        {
          simbolo: "Sb",
          nombre: "Antimonio",
          num_atomico: 51,
          masa_atomica: 121.76,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
        },
        {
          simbolo: "Te",
          nombre: "Telurio",
          num_atomico: 52,
          masa_atomica: 127.6,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
        },
        {
          simbolo: "I",
          nombre: "Yodo",
          num_atomico: 53,
          masa_atomica: 126.9044,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
        },
        {
          simbolo: "Xe",
          nombre: "Xenon",
          num_atomico: 54,
          masa_atomica: 131.293,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
        },
      ],
      [
        {
          simbolo: "Cs",
          nombre: "Cesio",
          num_atomico: 55,
          masa_atomica: 132.9054,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
        },
        {
          simbolo: "Ba",
          nombre: "Bario",
          num_atomico: 56,
          masa_atomica: 137.327,
          dibujar: true,
          tags: ["Alcalinotérreos"],
          color: "amber",
        },
        {
          simbolo: "Lu",
          nombre: "Lutecio",
          num_atomico: 71,
          masa_atomica: 174.9668,
          dibujar: false,
        },
        {
          simbolo: "Hf",
          nombre: "Hafnio",
          num_atomico: 72,
          masa_atomica: 178.49,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Ta",
          nombre: "Tantalio",
          num_atomico: 73,
          masa_atomica: 180.9478,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "W",
          nombre: "Wolframio",
          num_atomico: 74,
          masa_atomica: 183.84,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Re",
          nombre: "Renio",
          num_atomico: 75,
          masa_atomica: 186.207,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Os",
          nombre: "Osmio",
          num_atomico: 76,
          masa_atomica: 190.23,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Ir",
          nombre: "Iridio",
          num_atomico: 77,
          masa_atomica: 192.217,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Pt",
          nombre: "Platino",
          num_atomico: 78,
          masa_atomica: 195.084,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Au",
          nombre: "Oro",
          num_atomico: 79,
          masa_atomica: 196.97,
          serie_quimica: "Metal de Transición",
          estado_natural: "Sólido",
          color_info: "Amarillo Dorado",
          grupo: "11",
          dureza: "2.5 - 3",
          electronegatividad: "2.54",
          estado_de_oxidacion: "+1, +3",
          minerales_asoc:
            "Oro nativo con cuarzo (foto), Plata, Pirita, Arsenopirita, Limonita, Calcopirita",
          ubicacion_mundial: "Australia, Rusia, Brasil, Canadá, Estados Unidos",
          tipo_exploracion: "Subterránea",
          demanda: "Muy Alta",
          utilidad:
            "Ornamentación, Acuñación de monedas, joyería, fotografía, odontología, tratamiento contra el cáncer",
          dibujar: true,
          tags: ["Metales Transitorios", "En Ecuador"],
          color: "pink",
          src: "./assets/Au.jpg",
        },
        {
          simbolo: "Hg",
          nombre: "Mercurio",
          num_atomico: 80,
          masa_atomica: 200.59,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Tl",
          nombre: "Talio",
          num_atomico: 81,
          masa_atomica: 204.3833,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Pb",
          nombre: "Plomo",
          num_atomico: 82,
          masa_atomica: 207.2,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Bi",
          nombre: "Bismuto",
          num_atomico: 83,
          masa_atomica: 208.9804,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Po",
          nombre: "Polonio",
          num_atomico: 84,
          masa_atomica: 210,
          dibujar: true,
          tags: ["Metaloides"],
          color: "red",
        },
        {
          simbolo: "At",
          nombre: "Astato",
          num_atomico: 85,
          masa_atomica: 210,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
        },
        {
          simbolo: "Rn",
          nombre: "Radon",
          num_atomico: 86,
          masa_atomica: 220,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
        },
      ],
      [
        {
          simbolo: "Fr",
          nombre: "Francio",
          num_atomico: 87,
          masa_atomica: 223,
          dibujar: true,
          tags: ["Alcalinos"],
          color: "blue",
        },
        {
          simbolo: "Ra",
          nombre: "Radio",
          num_atomico: 88,
          masa_atomica: 226,
          dibujar: true,
          tags: ["Alcalinotérreos"],
          color: "amber",
        },
        {
          simbolo: "Lr",
          nombre: "Laurencio",
          num_atomico: 103,
          masa_atomica: 262,
          dibujar: false,
        },
        {
          simbolo: "Rf",
          nombre: "Rutherfordio",
          num_atomico: 104,
          masa_atomica: 261,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Db",
          nombre: "Dubnio",
          num_atomico: 105,
          masa_atomica: 262,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Sg",
          nombre: "Seaborgio",
          num_atomico: 106,
          masa_atomica: 266,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Bh",
          nombre: "Bohrio",
          num_atomico: 107,
          masa_atomica: 264,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Hs",
          nombre: "Hassio",
          num_atomico: 108,
          masa_atomica: 277,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Mt",
          nombre: "Meitnerio",
          num_atomico: 109,
          masa_atomica: 268,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Ds",
          nombre: "Darmstatio",
          num_atomico: 110,
          masa_atomica: 271,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Rg",
          nombre: "Roenfgenio",
          num_atomico: 111,
          masa_atomica: 272,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Cn",
          nombre: "Copernicio",
          num_atomico: 112,
          masa_atomica: 285,
          dibujar: true,
          tags: ["Metales Transitorios"],
          color: "pink",
        },
        {
          simbolo: "Nh",
          nombre: "Nihonio",
          num_atomico: 113,
          masa_atomica: 284,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Fl",
          nombre: "Flerovio",
          num_atomico: 114,
          masa_atomica: 289,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Mc",
          nombre: "Moscovio",
          num_atomico: 115,
          masa_atomica: 288,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Lv",
          nombre: "Livermorio",
          num_atomico: 116,
          masa_atomica: 292,
          dibujar: true,
          tags: ["Otros metales"],
          color: "teal",
        },
        {
          simbolo: "Ts",
          nombre: "Teneso",
          num_atomico: 117,
          masa_atomica: 294,
          dibujar: true,
          tags: ["Halógenos"],
          color: "indigo",
        },
        {
          simbolo: "Og",
          nombre: "Oganeson",
          num_atomico: 118,
          masa_atomica: 294,
          dibujar: true,
          estado: "Gaseoso",
          tags: ["Gases Nobles"],
          color: "purple",
        },
      ],
    ],
    extra_elements: [
      [
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          simbolo: "La",
          nombre: "Lantano",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Ce",
          nombre: "Cerio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Pr",
          nombre: "Praseodimio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Nd",
          nombre: "Neodimio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Pm",
          nombre: "Prometio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Sm",
          nombre: "Samario",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Eu",
          nombre: "Europio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Gd",
          nombre: "Gadolinio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Tb",
          nombre: "Terbio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Dy",
          nombre: "Disprosio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Ho",
          nombre: "Holmio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Er",
          nombre: "Erbio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Tm",
          nombre: "Tulio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Yb",
          nombre: "Yterbio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          simbolo: "Lu",
          nombre: "Lutecio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Lantanidos"],
          color: "lime",
        },
        {
          dibujar: false,
        }
      ],
      [
        {
          dibujar: false,
        },
        {
          dibujar: false,
        },
        {
          simbolo: "Ac",
          nombre: "Actinio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Th",
          nombre: "Torio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Pa",
          nombre: "Protactinio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "U",
          nombre: "Uranio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Np",
          nombre: "Neptunio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Pu",
          nombre: "Plutonio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Am",
          nombre: "Americio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Cm",
          nombre: "Curio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Bk",
          nombre: "Berkelio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Cf",
          nombre: "Californio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Es",
          nombre: "Eistenio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Fm",
          nombre: "Fermio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Md",
          nombre: "Mendelevio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "No",
          nombre: "Nobelio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          simbolo: "Ac",
          nombre: "Actinio",
          num_atomico: 57,
          masa_atomica: 138.91,
          dibujar: true,
          estado: "Solido",
          tags: ["Actinidos"],
          color: "brown",
        },
        {
          dibujar: false,
        }
      ],
    ],
    groups: [
      "En Ecuador",
      "Alcalinos",
      "Alcalinotérreos",
      "Otros metales",
      "Metaloides",
      "Otros no metales",
      "Halógenos",
      "Gases Nobles",
      "Metales Transitorios",
    ],
  }),
  methods: {
    changeCategory(category) {
      this.selectedCategory = category;
    },
    getColor(col) {
      if (this.selectedCategory == null) {
        return col.color;
      }
      if (col.tags) {
        if (col.tags.indexOf(this.selectedCategory) >= 0) {
          return col.color;
        }
      }
      return this.unselectedColor;
    },
  },
};
</script>

<style scoped>
.el-nombre {
  font-size: 55%;
  color: black;
}

.el-num-atom {
  font-size: 70%;
  text-align: center;
  color: black;
}

.el-simbolo {
  text-align: center;
}

.box {
  max-width: 70px;
  width: 40px;
  text-align: center;
}

.v-tooltip__content {
  font-size: 50px !important;
  background-color: white;
}

.v-card-content {
  display: flex;
  width: 100%;
  margin: auto;
  align-items: center;
  justify-content: center;
}

.description {
  font-size: medium;
}

.move-right {
  display: block;
  margin: auto;
}

.bordeado {
  border: 1px solid black;
}

.background {
  background-color: #9370db;
}
</style>