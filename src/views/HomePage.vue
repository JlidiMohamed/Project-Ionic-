<template>
  <ion-page>
    <ion-header translucent>
        <ion-toolbar>
          <ion-title class="ion-text-center">Mon Formulaire</ion-title>
        </ion-toolbar>
      </ion-header>
    
    <ion-content :fullscreen="true">
     
      <ion-item>
            <ion-label >Civilité</ion-label>
            <ion-select v-model="civilite">
      <ion-select-option value="Mr">Mr</ion-select-option>
      <ion-select-option value="Mme">Mme</ion-select-option>
    </ion-select>
          </ion-item>
          <ion-item>
    <ion-label position="floating">Nom</ion-label>
    <ion-input v-model="nom"></ion-input>
  </ion-item>
  <ion-item>
    <ion-label position="floating">Prenom</ion-label>
    <ion-input v-model="prenom"></ion-input>
  </ion-item>
          <ion-item >
            <ion-label>Matieres</ion-label>
            <ion-item v-for="(matiere, index) in matieres" :key="index">
              <ion-checkbox slot="start" :value="matiere.label" v-model="matiere.checked"></ion-checkbox>
            <ion-label>{{ matiere.label }}</ion-label>
            </ion-item>
          </ion-item>
      <ion-list>
       
       <ion-radio-group v-model="specialite">
        <ion-label>Specialites</ion-label>
        <ion-item v-for="(specialite, index) in specialites" :key="index">
          <ion-radio slot="start" :value="specialite" ></ion-radio>
          <ion-label>{{ specialite }}</ion-label>
           </ion-item>
           <ion-text class="ion-text-center" >
          <ion-item>
          <ion-button
            class="primary"
            :router-link="{
        name: 'affichage',

        params: {
          civilite: civilite,
          nom: nom,
          prenom: prenom,
          specialite: specialite,
          Tmatiere: matieres.filter(matiere => matiere.checked).map(matiere => matiere.label),
        },
      }"
            >Ajouter</ion-button
          >
        </ion-item></ion-text>
        
           

          

          
        
       </ion-radio-group>
    </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar ,IonCheckbox,IonRadioGroup, IonList, IonRadio, IonLabel ,IonInput,IonSelectOption,IonSelect, IonButton} from '@ionic/vue';
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'HomePage',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonCheckbox,
    IonRadioGroup, 
    IonList, 
    IonRadio,
    IonLabel,
    IonInput,
    IonSelectOption,
    IonSelect, 
    IonButton
  },
   data() {
    return {
      civilite:"" ,
      matieres:[],
      nom:"",
      prenom:"",
      specialite:"",
      specialites:[]

    };
  },
  methods: {
    /* afficher() {
      this.router.push({
        name: "affichage",

        params: {
          civilite: this.civilite,
          nom: this.nom,
          prenom: this.prenom,
          specialite: this.specialite,
          Tmatiere: this.matieres.filter(matiere => matiere.checked).map(matiere => matiere.label),
        },
      });
    }, */ 
    fetchdata() {
      axios.get("http://localhost:3000/specialites").then((response) => {
        this.specialites = response.data;
      });
      axios
      .get("http://localhost:3000/matieres").then((response) => {
        this.matieres = response.data.map(function(matiere:string){
          return {
            label: matiere,
            checked: false
          };
        });
      });
    },
  },
  created() {
    this.fetchdata();
  },

  
  
});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
:root {
        --ion-safe-area-top: 20px;
        --ion-safe-area-bottom: 22px;
      }
</style>