<template>
  <v-app id="app">
    <v-card  color="grey lighten-4" flat height="65px" tile>

      <v-app-bar color="deep-purple" dark>
        <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
  
        <v-toolbar-title>
          <v-img max-height="156" max-width="203" src="./assets/logo_notredame.jpg"></v-img>
        </v-toolbar-title>

        <v-container>
          <v-row> 
            <v-col cols="4"></v-col>
          </v-row>
          <v-row>
            <v-col cols="4"></v-col>
          <v-col cols="4">
            <v-combobox v-model="selectRegional" :items="itemsRegional" label="Regional" multiple outlined dense></v-combobox>
          </v-col>
          <v-col cols="4">
            <v-combobox v-model="selectLojas" :items="itemsLojas" label="Lojas" multiple outlined dense></v-combobox>
          </v-col>
          </v-row>
        </v-container>

        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">          
            <v-btn icon v-bind="attrs" v-on="on">
              <v-icon color="yellow">mdi-alert-decagram</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item v-for="(item, index) in itemsMenuAlerta" :key="index" three-line>

                <v-list-item-content>
                  <v-list-item-title>{{ item.loja }} </v-list-item-title>
                  <v-list-item-subtitle>{{ item.data }}</v-list-item-subtitle>
                </v-list-item-content>
                <v-chip  class="ma-1">
                      <v-icon left>mdi-timer</v-icon>
                      2 min
                  </v-chip>
                <v-chip  class="ma-1" color="red" text-color="white">
                      <v-icon left>mdi-thermometer-plus</v-icon>
                      {{ item.maxima }}
                  </v-chip>
                  <v-chip  class="ma-1" color="blue" text-color="white">
                    <v-icon left>mdi-thermometer-minus</v-icon>
                    {{ item.minima }}
                </v-chip>
            </v-list-item>
          </v-list>
        </v-menu>
        <v-btn icon>
            <v-icon>mdi-account-circle</v-icon>
        </v-btn>    
        <v-btn icon>
          <v-icon>mdi-logout</v-icon>
        </v-btn>
      
      </v-app-bar>
  
    </v-card>   

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group v-model="group" active-class="deep-purple--text text--accent-4">
            <v-list-item v-for="(item, index) in itemsMenu" :key="index">
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <div id="myMap" style="position:relative;width:100%;height:100%;z-index:1;"></div>

  </v-app>
</template>

<script>
export default {
  name: 'App',

  data: () => ({

    drawer: false,
    group: null,
    
    selectRegional: [],
    itemsRegional: [
      'GND São Paulo',
      'GND Rio de janeiro'
    ],

    selectLojas: [],
    itemsLojas: [
      'ND - São Paulo',
      'ND - Rio de janeiro',
      'ND - Nova Iguaçu',
      'ND - Duque de Caxias'
    ],

    itemsMenuAlerta: [
      { loja: 'Porto BR', maxima:'25.1°C ', minima:'14.3°C', data:'10/01/2020 14:30:13' },
      { loja: 'Farmacia Novo Horizonte', maxima:'25.1°C', minima:'14.3°C', data:'10/01/2020 14:30:13' },
      { loja: 'Suermercado Mundial', maxima:'25.1°C', minima:'14.3°C', data:'10/01/2020 14:30:13' },
    ],

    itemsMenu: [
      { title: 'Home', icon: 'mdi-home' },
      { title: 'Alarme', icon: 'mdi-alarm-light' },
      { title: 'Mapas', icon: 'mdi-map' },
      { title: 'Relatórios', icon: 'mdi-file-chart' },
    ]
    
  }),
};
</script>
