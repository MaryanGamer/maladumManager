<script setup>
import { ref, computed } from 'vue'
import abilityMaladumViewer from './abilityMaladumViewer.vue'

//let id = 0


const availClasses = ref([
{
   "nom":"Aspirant","classe EN":"Contender","origin":"","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "ajout de des rouge","type":"" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Hyper conscience","type":"Sort" },"cursusMaxLevel":"-"},
       {"abilityKey" :  { "nom": "Adversaire digne de ce nom","type":"Pouvoir" },"cursusMaxLevel":"-"},
       {"abilityKey" :  { "nom": "Acrobatie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Eloquence","type":"Compétence" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Constant","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Don tactique","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intimidation","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Carnage","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Assassin","classe EN":"","origin":"Base game","cost":"7","aptitudes" : [

       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Arts martiaux","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Acrobatie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intouchable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Désarmement","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tir Vicieux","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Récupération Rapide","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Barbare","classe EN":"","origin":"Base game","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "Attaque mains nues","type":"Pouvoir" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Force","type":"Sort" },"cursusMaxLevel":"-"},

       {"abilityKey" :  { "nom": "Frénésie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Assaut Brutal","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Carnage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Indomptable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Arts martiaux","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intimidation","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Charlatan","classe EN":"Deceiver","origin":"","cost":"7","aptitudes" : [

       ]
},

{
   "nom":"Conservateur","classe EN":"Curator","origin":"","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "Moins de PV","type":"Pouvoir" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Plus de Talent","type":"Pouvoir" },"cursusMaxLevel":"2"},

       {"abilityKey" :  { "nom": "Connaissance","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Herboristerie","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Héros malgré lui","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Forge","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Plonger à couvert","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Don tactique","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Troc","type":"Compétence" },"cursusMaxLevel":"2"},

       ]
},

{
   "nom":"Druide","classe EN":"","origin":"","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "Magie","type":"Magie" },"cursusMaxLevel":"8"},

       {"abilityKey" :  { "nom": "Pistage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Distraction","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Uni avec la nature","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Esprit renforcé","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Remède Naturel","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Embuscade","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Ermitte","classe EN":"Eremite","origin":"","cost":"7","aptitudes" : [

       ]
},

{
   "nom":"Escroc","classe EN":"Swindler","origin":"","cost":"11","aptitudes" : [
       {"abilityKey" :  { "nom": "Illusion","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "je sais pas","type":"Pouvoir" },"cursusMaxLevel":"-"},

       {"abilityKey" :  { "nom": "Eloquence","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Désarmement","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Doigts agiles","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Distraction","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur d'élite","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Tir Vicieux","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Artiste","type":"Compétence" },"cursusMaxLevel":"1"},

       ]
},

{
   "nom":"Eudaemon","classe EN":"","origin":"","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "Magie","type":"Magie" },"cursusMaxLevel":"10"},

       {"abilityKey" :  { "nom": "Maitrise de la Malacyte","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Indomptable","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Inspirant","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Esprit renforcé","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Carnage","type":"Compétence" },"cursusMaxLevel":""},

       ]
},

{
   "nom":"Forgeron","classe EN":"","origin":"","cost":"9","aptitudes" : [
       {"abilityKey" :  { "nom": "Affaiblissement d'armure","type":"Sort" },"cursusMaxLevel":"-"},

       {"abilityKey" :  { "nom": "Forge","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Constant","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Indomptable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur Expert","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Troc","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Ficelles du métier","type":"Compétence" },"cursusMaxLevel":"2"},

       ]
},

{
   "nom":"Maestro","classe EN":"Maestro","origin":"","cost":"54","aptitudes" : [
       {"abilityKey" :  { "nom": "Relancer","type":"Pouvoir" },"cursusMaxLevel":"-"},

       {"abilityKey" :  { "nom": "Artiste","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Héros malgré lui","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Inspirant","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Troc","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intouchable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Persuasion","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Récupération Rapide","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Magus","classe EN":"","origin":"","cost":"21","aptitudes" : [

       ]
},

{
   "nom":"Mentor","classe EN":"","origin":"","cost":"5","aptitudes" : [

       ]
},

{
   "nom":"Mercenaire","classe EN":"Sellsword","origin":"Base game","cost":"2","aptitudes" : [
       {"abilityKey" :  { "nom": "Pt Action supplémentaire","type":"Pouvoir" },"cursusMaxLevel":"1"},

       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Frénésie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tir de Riposte","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur d'élite","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Entrainement","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Récupération rapide","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Paladin","classe EN":"","origin":"","cost":"2","aptitudes" : [
       {"abilityKey" :  { "nom": "Magie","type":"Magie" },"cursusMaxLevel":"8"},
       {"abilityKey" :  { "nom": "Soin","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Focalisation","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Force","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Endurcissement","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Calme","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Bénédiction","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Force d'âme","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Empathie","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Renforcement","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Epuisement","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Réveil","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Resistance partagée","type":"Sort" },"cursusMaxLevel":""},

       {"abilityKey" :  { "nom": "Inspiration","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Marchandage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Insensible","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Inamovible","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Désarmement","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Entourloupe","type":"Compétence" },"cursusMaxLevel":"2"},
       ]
},

{
   "nom":"Pillard","classe EN":"Scavenger","origin":"","cost":"2","aptitudes" : [
       {"abilityKey" :  { "nom": "Rapide","type":"Pouvoir" },"cursusMaxLevel":"1"},

       {"abilityKey" :  { "nom": "Acrobatie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Pied agile","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Arts martiaux","type":"Compétence" },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Ficelles du métier","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Doigts agiles","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intouchable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Troc","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Prymorist","classe EN":"","origin":"","cost":"2","aptitudes" : [
       {"abilityKey" :  { "nom": "Magie","type":"Magie" },"cursusMaxLevel":"12"},

       {"abilityKey" :  { "nom": "Manipulation Pouvoir","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Maitrise de la Malacyte","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Intouchable","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Esprit renforcé","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Remède Naturel","type":"Compétence" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Tir de Riposte","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Ranger","classe EN":"","origin":"Base game","cost":"0","aptitudes" : [
       {"abilityKey" :  { "nom": "Embuscade","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Camouflage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Pistage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur Expert","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Récupération rapide","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Uni avec la nature","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Roublard","classe EN":"Rogue","origin":"Base game","cost":"54","aptitudes" : [
       {"abilityKey" :  { "nom": "Ouverture","type":"Sort" },"cursusMaxLevel":"1"},

       {"abilityKey" :  { "nom": "Doigts agiles","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Ficelles du métier","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Distraction","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Entourloupe","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Camouflage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Plonger à couvert","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Sorcier","classe EN":"Warlock","origin":"","cost":"214","aptitudes" : [

       ]
},

{
   "nom":"Stratège","classe EN":"Strategist","origin":"","cost":"5","aptitudes" : [
       {"abilityKey" :  { "nom": "Préscience","type":"Sort" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Résistance partagée","type":"Sort" },"cursusMaxLevel":"4"},
       {"abilityKey" :  { "nom": "XP gratuits","type":"Pouvoir" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom":"Vantardise","type":"Compétence"  },"cursusMaxLevel":"2"},
       {"abilityKey" :  { "nom": "Tir de Riposte","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Diversion","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur Expert","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Prêt à tout","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Don tactique","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Formation","type":"Compétence" },"cursusMaxLevel":"3"}
       ]
},

{
   "nom":"Vagabond","classe EN":"Rambler","origin":"extension","cost":"2","aptitudes" : [
       {"abilityKey" :  { "nom": "Detect","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Recovery","type":"Sort" },"cursusMaxLevel":""},
       {"abilityKey" :  { "nom": "Immunité (Handicap)","type":"Pouvoir" },"cursusMaxLevel":""},

       {"abilityKey" :  { "nom": "Uni avec la nature","type":"Compétence" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Intouchable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Herboristerie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Promptitude","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Pistage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Récupération Rapide","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Ficelles du métier","type":"Compétence" },"cursusMaxLevel":"3"},
       ]
},

{
   "nom":"Tireur d'élite","classe EN":"","origin":"KS","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "cible","type":"Pouvoir" },"cursusMaxLevel":""},

       {"abilityKey" :  { "nom": "Tir Vicieux","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur d'élite","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tireur Expert","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Tir de Riposte","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Embuscade","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Plonger à couvert","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Pied agile","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"3"},

       ]
},

{
   "nom":"Gardien","classe EN":"Guardian","origin":"KS","cost":"7","aptitudes" : [
       {"abilityKey" :  { "nom": "PV Sup","type":"Pouvoir" },"cursusMaxLevel":"1"},

       {"abilityKey" :  { "nom": "Carnage","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Constant","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Indomptable","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Récupération rapide","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Frénésie","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Assaut Brutal","type":"Compétence" },"cursusMaxLevel":"3"},
       {"abilityKey" :  { "nom": "Prêt à tout","type":"Compétence" },"cursusMaxLevel":"2"},

       ]
},

])




const availCompanions = ref([
  {
    "Nom": "Ariah",
    "Cost": 73,
    "Life": "1/2/3/6",
    "Talent": "1/5",
    "Magie": "2/4",
    "Action": "2/2",
    "XPs": "2/6/4/5/3/3",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Don tactique","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1"},
       {"abilityKey" :  { "nom": "Tireur d'élite","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":true},
       ]
  },

  {
    "Nom": "Artain",
    "Cost": 61,
    "Life": "1/2/3/5",
    "Talent": "2/4",
    "Magie": "2/5",
    "Action": "2/2",
    "XPs": "1/4/4/3/3",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Artiste","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "2"},
       ]
  },
  {
    "Nom": "Beren",
    "Cost": 71,
    "Life": "1/2/3/5",
    "Talent": "1/3",
    "Magie": "3/7",
    "Action": "2/2",
    "XPs": "4/6/5/3/3/3",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Remède Naturel","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1"},
       ],

  },
  {
    "Nom": "Brahm",
    "Cost": 90,
    "Life": "1/2/4/6",
    "Talent": "2/5",
    "Magie": "2/4",
    "Action": "2/3",
    "XPs": "4/6/5/5/4/3",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Insensible à la Terreur","type":"Pouvoir" },"cursusMaxLevel":"1"},
       {"abilityKey" :  { "nom": "Maitrise des Armes","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1","cursusSlotArmor":false},
       {"abilityKey" :  { "nom": "Tireur Expert","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":true},
       ]
  },
  {
    "Nom": "Callan",
    "Cost": 54,
    "Life": "1/2/4/5",
    "Talent": "1/4",
    "Magie": "1/3",
    "Action": "2/2",
    "XPs": "1/4/3/4/2/0",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Frénésie","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1"},
       ],
  },
  {
    "Nom": "Chiau",
    "Cost": 71,
    "Life": "1/2/3/4",
    "Talent": "2/5",
    "Magie": "3/7",
    "Action": "2/2",
    "XPs": "4/6/3/4/5/0",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Amélioration de Malacyte","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1"},
       ],
  },
  {
    "Nom": "Emmerik",
    "Cost": "",
    "Life": "1/2/3/5",
    "Talent": "1/3",
    "Magie": "3/6",
    "Action": "2/?",
    "XPs": "1/6/5/3/3/0",
    "aptitudes" : [

       ],
  },
  {
    "Nom": "Galen",
    "Cost": "",
    "Life": "1/2/3/5",
    "Talent": "2/5",
    "Magie": "2/4",
    "Action": "2/3",
    "XPs": "1/5/4/3/4/0",
    "aptitudes" : [
       {"abilityKey" :  { "nom": "Initiative","type":"Pouvoir" },"cursusSlotArmor":true},
       ],

  },
  {
    "Nom": "Greet",
    "Cost": "",
    "Life": "1/2/3/4",
    "Talent": "2/5",
    "Magie": "1/4",
    "Action": "2/3",
    "XPs": "2/5/5/4/3/2",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Troc","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":false},
    {"abilityKey" :  { "nom": "Ficelles du métier","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":false},
       ],
  },
  {
    "Nom": "Gromgar",
    "Cost": 73,
    "Life": "1/2/5/7",
    "Talent": "1/3",
    "Magie": "1/3",
    "Action": "2/2",
    "XPs": "2/4/4/4/3/0",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Attaque mains nues","type":"Pouvoir" },"cursusMaxLevel":"2"},
    {"abilityKey" :  { "nom": "Récupération rapide","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1","cursusSlotArmor":true},
    {"abilityKey" :  { "nom": "Taille","type":"Pouvoir" },"cursusMaxLevel":"2"},
       ],

  },
  {
    "Nom": "Hendley",
    "Cost": "",
    "Life": "1/2/4/7",
    "Talent": "3/6",
    "Magie": "1/3",
    "Action": "2/?",
    "XPs": "3/4/4/3/4/0",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Vision nocturne","type":"Pouvoir" }},
    {"abilityKey" :  { "nom": "forge","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1"}
       ],
  },
  {
    "Nom": "Kaan",
    "Cost": 73,
    "Life": "1/2/5/6",
    "Talent": "1/3",
    "Magie": "2/6",
    "Action": "2/2",
    "XPs": "1/5/4/4/5/0",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Attaque mains nues","type":"Pouvoir" },"cursusMaxLevel":"3"},
    {"abilityKey" :  { "nom": "Taille","type":"Pouvoir" },"cursusMaxLevel":"2"},
    {"abilityKey" :  { "nom": "Assaut brutal","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1","cursusSlotArmor":true}
       ],
  },
  {
    "Nom": "Kriga",
    "Cost": 73,
    "Life": "1/2/4/6",
    "Talent": "2/6",
    "Magie": "1/3",
    "Action": "2/2",
    "XPs": "3/5/4/4/3/2",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Implacable","type":"Pouvoir" }},
       ],
  },
  {
    "Nom": "Merinda",
    "Cost": 80,
    "Life": "1/2/4/6",
    "Talent": "2/6",
    "Magie": "1/3",
    "Action": "2/3",
    "XPs": "3/5/4/3/3/2",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Attaque mains nues","type":"Pouvoir" },"cursusMaxLevel":"1"},
    {"abilityKey" :  { "nom": "Maitre d'armes","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1","cursusSlotArmor":false},
    {"abilityKey" :  { "nom": "Pieds agiles","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":true}

       ],

  },
  {
    "Nom": "Moranna",
    "Cost": 80,
    "Life": "1/2/3/4",
    "Talent": "2/4",
    "Magie": "2/7",
    "Action": "2/3",
    "XPs": "5/6/5/4/3/3",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Acrobatie","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":true},
    {"abilityKey" :  { "nom": "Maitrise de la Malacyte","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "1","cursusSlotArmor":false},
    {"abilityKey" :  { "nom": "Indomptable","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":false}
       ],

  },
  {
    "Nom": "Numinor",
    "Cost": "",
    "Life": "1/2/4/7",
    "Talent": "?/4",
    "Magie": "?/5",
    "Action": "2/?",
    "XPs": "1/2/5/5/5/5",
    "aptitudes" : [
       ],

  },
  {
    "Nom": "Phedra",
    "Cost": "",
    "Life": "1/2/?/?",
    "Talent": "?/?",
    "Magie": "?/?",
    "Action": "?/?",
    "XPs": "1/2/5/5/5/5",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Arts Interdits","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":true},
       ],
  },
  {
    "Nom": "Syrio",
    "Cost": 64,
    "Life": "1/2/4/6",
    "Talent": "1/4",
    "Magie": "1/4",
    "Action": "2/2",
    "XPs": "3/5/4/4/3/0",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Reflexes","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1","cursusSlotArmor":false},
    {"abilityKey" :  { "nom": "Rapide","type":"Pouvoir" },"cursusMaxLevel":"1","cursusSlotArmor":true},
       ],
  },
  {
    "Nom": "Unger",
    "Cost": "",
    "Life": "1/2/3/5",
    "Talent": "2/5",
    "Magie": "2/4",
    "Action": "2/3",
    "XPs": "2/6/5/4/4/0",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Détection","type":"Sort" }},
    {"abilityKey" :  { "nom": "Entourloupe","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "1"}
    ]
  },
  {
    "Nom": "Corazon",
    "Cost": 83,
    "Life": "1/2/3/3",
    "Talent": "2/6",
    "Magie": "3/7",
    "Action": "2/2",
    "XPs": "4/6/6/3/4/4",
    "aptitudes" : [
    {"abilityKey" :  { "nom": "Persuasion","type":"Compétence" },"cursusMaxLevel":"2","cursusInitialLevel" : "2","cursusSlotArmor":false},
    {"abilityKey" :  { "nom": "Camouflage","type":"Compétence" },"cursusMaxLevel":"1","cursusInitialLevel" : "0","cursusSlotArmor":true},
    {"abilityKey" :  { "nom": "Malédiction","type":"Sort" },"cursusMaxLevel":"1"},
       ],

  }
])



async function fetchClassesData() {
  //todoData.value = null
  const res = await fetch(
    `./data/classes.json`
  )
  //console.log(res)

  var l_text = await res.text()
  //console.log(l_text)
  availClasses.value = JSON.parse(l_text)
  //console.log(availClasses.value)
}

fetchClassesData()


async function fetchCompanionsClassesData() {
  //todoData.value = null
  const res = await fetch(
    `./data/companions.json`
  )

  //console.log(res)

  var l_text = await res.text()
  //console.log(l_text)
  availCompanions.value = JSON.parse(l_text)
  //console.log(availCompanions.value)


}
fetchCompanionsClassesData()


// affiche la liste des candidates ou pas
const hideList = ref(false)
const hideClasses = ref(false)
const hideCharacters = ref(false)
// affichage d'un candidat sélectionné ou pas
const availCompanionIsFocus = ref(false)
const availClasseIsFocus = ref(false)
// candidat
let availCompanionFocus = new Object()
let availClasseFocus= new Object()

// element de remontée au parent
const emit = defineEmits(['selectedCandidate'])

// referentiel des abilités
//const abilityReferentiel = inject('abilityReferential')
//console.log("referentiel abilités dans addMember : ",abilityReferentiel.value)
//console.log("valeur referentiel abilités dans addMember : ",abilityReferentiel)

// on veut afficher les candidats. On affiche plus un focus eventuel
function showAvailCompanions() {
  hideList.value = !hideList.value
  availCompanionIsFocus.value = false
}
// lorsqu'on veut faire un focus sur un candidat
function focusOn(availCompanion) {
  availCompanionIsFocus.value = false
  availCompanionFocus = availCompanion
  //console.log ("compagnon availCompanion en focus : ",availCompanion)
  //console.log ("availCompanionFocus : ",availCompanionFocus)
  availCompanionIsFocus.value = true
}
function selectCandidate() {
  // on remonter le candidat, qu'on construit vite fait
  let candidate = {availCompanion : availCompanionFocus,classe:availClasseFocus}

  //console.log ("candidat remonté : ",candidate)
  emit('selectedCandidate', candidate)
  availCompanionIsFocus.value = false
  availClasseIsFocus.value=false
  //console.log("referentiel abilités dans addMember/selectCandidate : ",abilityReferentiel.value)

}

function showAvailCharacters() {
  hideCharacters.value = !hideCharacters.value

}
function showAvailClasses() {
  hideClasses.value = !hideClasses.value
  availClasseIsFocus.value = false
}

showAvailCharacters
// lorsqu'on veut faire un focus sur une classe
function focusOnClass(classeFocus) {
  availClasseIsFocus.value = false
  availClasseFocus = classeFocus
  //console.log ("compagnon availCompanion en focus : ",availCompanion)
  //console.log ("availCompanionFocus : ",availCompanionFocus)
  availClasseIsFocus.value = true
}

const focusOnCompanionAndClasse = computed(() => {
  if (availClasseIsFocus.value & availCompanionIsFocus.value)
  { return true}
  else
  {return false}
})
const companionBaseLife = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Life[4]}
  else
  {return ""}
})
const companionMaxLife = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Life[6]}
  else
  {return ""}
})

const companionBaseTalents = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Talent[0]}
  else
  {return ""}
})
const companionMaxTalents = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Talent[2]}
  else
  {return ""}
})

const companionBaseMagic = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Magie[0]}
  else
  {return ""}
})
const companionMaxMagic = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Magie[2]}
  else
  {return ""}
})

const companionBaseActions = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Action[0]}
  else
  {return ""}
})
const companionMaxActions = computed(() => {
  if (availCompanionIsFocus.value)
  { return availCompanionFocus.Action[2]}
  else
  {return ""}
})


function isNumeric (suspect) {
  return (!isNaN(parseFloat(suspect)) && isFinite(suspect));
}

</script>

<template>
<div class="pure-g global-recruit" >
  <div class="pure-u-1" >
    <button @click="showAvailCompanions">
      {{ hideList ? '-' : '+' }}
    </button> Recrutement
    <div class="pure-u-1" v-if="hideList">
      <div class="pure-g alignGlobal" >
        <div class="pure-u-1-2 alignGlobal" >
          <button @click="showAvailCharacters">
            {{ hideCharacters ? 'cacher les Personnages' : 'Personnages disponibles' }}
          </button>
        </div>
        <div class="pure-u-1-2 alignGlobal">
          <button @click="showAvailClasses">
          {{ hideClasses ? 'cacher les carrières' : 'Selectionner une carrière' }}
          </button>
        </div>
        <div class="pure-u-1-2"  v-if="hideCharacters"  >
          <span v-for="companion in availCompanions" :key="companion.Nom">
            <button @click="focusOn(companion)">{{companion.Nom}}</button>
          </span>
        </div>
        <div class="pure-u-1-2"   v-else>

        </div>

        <div class="pure-u-1-2 "   v-if="hideClasses">
          <span v-for="classe in availClasses" :key="classe.nom">
            <button @click="focusOnClass(classe)">{{classe.nom}}</button>
          </span>
        </div>
        <div class="pure-u-1-2"   v-else>

          </div>
      </div>
      <div class="pure-g" v-if="availCompanionIsFocus">
        <div class="pure-u-1-2" >
          Compagnion sélectionné : {{  availCompanionFocus.Nom }} - Valeur : {{  availCompanionFocus.Cost }} G
          <br/>
          Vitalité : {{ companionBaseLife }} (Max {{ companionMaxLife }} ) - XPs =  {{  availCompanionFocus.XPs }}
          <br/>
          Talents : {{ companionBaseTalents }} (Max {{ companionMaxTalents }} ) - Magie =  {{  companionBaseMagic }}
          (Max {{ companionMaxMagic }} ) - Actions : {{ companionBaseActions }} (Max {{ companionMaxActions }} )

          <ul>
            <li v-for="Aptitude in availCompanionFocus.aptitudes" :key="Aptitude.abilityKey.nom">
              <span class=tooltip>
                {{ Aptitude.abilityKey.type }}  : {{  Aptitude.abilityKey.nom }}
                <abilityMaladumViewer :abilityKeyNom="Aptitude.abilityKey.nom"  :abilityKeyType="Aptitude.abilityKey.type" :tooltipOnLeft="false" />
              </span>
              <span v-if="Aptitude.abilityKey.type=='Compétence'">
                (
                <span v-if="isNumeric(Aptitude.cursusInitialLevel)"> {{ Aptitude.cursusInitialLevel }} /  </span>
                <span v-else> Max </span>
                {{  Aptitude.cursusMaxLevel }}
                )
              </span>
              <span v-else> ({{  Aptitude.cursusMaxLevel }})</span>
            </li>
          </ul>
        </div>
        <div class="pure-u-1-2" v-if="availClasseIsFocus">
          Classe sélectionnée : {{  availClasseFocus.nom }} - {{  availClasseFocus.cost }} G
          <ul>
            <li v-for="Aptitude in availClasseFocus.aptitudes" :key="Aptitude.abilityKey.nom">
              <span class=tooltip>
                {{  Aptitude.abilityKey.type }}  : {{  Aptitude.abilityKey.nom }} <span v-if="isNumeric(Aptitude.cursusMaxLevel)"> (<span v-if="Aptitude.abilityKey.type=='Compétence'">Max </span><span v-if="Aptitude.abilityKey.type=='Sort'">Niveau </span>{{  Aptitude.cursusMaxLevel }})</span>
                <abilityMaladumViewer :abilityKeyNom="Aptitude.abilityKey.nom"  :abilityKeyType="Aptitude.abilityKey.type" :tooltipOnLeft="true" />
              </span>
            </li>
          </ul>
        </div>

        <div class="pure-u-1" v-if="focusOnCompanionAndClasse">
          <button @click="selectCandidate">Intégrer ce candidat</button>
        </div>
      </div>
    </div>
  </div>
</div>

 </template>
