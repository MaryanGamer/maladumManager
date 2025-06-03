<script setup>
//NON UTILISE
import { ref,onMounted } from 'vue'
// voir abilityaladum.vue pour le format des objets
// on récupère un objet XP (dépensé ou pas), et on va afficher l'info correctement, et eventuiellement propose du'iliser l'XP non dépensé.

// on doit récupérer le membre en question.
const member = defineModel()
// on récupère en props le N° d'XP concerné (on ira le chercher dans le member.
const props = defineProps({
  indexXP: Number
})



// format de propopsition de formation tableau de  {"abilityKey" :  { "nom":"Plonger à couvert","type":"Compétence"  },newLevel : "1"}
const l_upgradeProposals = ref([])
let l_abilityFoundInSkillcurrentLevel = Object

function updateUpgradeProposalList() {
  // on vide le tableau des propositions
  l_upgradeProposals.value = []
  // on liste le plan de carrière.
  // pour chacun option de carrière, on regarde si il a entamé l'arbre de compétence
  let l_abilityCursus = Object
  // si oui, on propose le niveau suivant (si le rank le permet et si il a pas le max)
  // si non, on propose le 1er niveau
  // proposer = ajouter la proposition dans le tableau de propositions d'upgrade
  for (let pas = 0; pas < member.value.candidate.classe.aptitudes.length; pas++) {
    l_abilityCursus = member.value.candidate.classe.aptitudes[pas]
    console.log("abilityYtraining1XP - check cursus : ",l_abilityCursus)
    // scan skillCurrentLevel si on trouve la compétence (et si c'est une compétence.)
    if (l_abilityCursus.abilityKey.type == "Compétence")
    {
      l_abilityFoundInSkillcurrentLevel = null
      console.log("abilityYtraining1XP - on va chercher dans ",member.value.memberInfos.skillCurrentLevels)
      console.log("si on trouve ",l_abilityCursus.abilityKey)
      l_abilityFoundInSkillcurrentLevel = member.value.memberInfos.skillCurrentLevels.filter((t) => t.abilityKey == l_abilityCursus.abilityKey)
      if (l_abilityFoundInSkillcurrentLevel.length == 0)
      {
        // rien n'a été investi sur cette compétence. on peut proposer le niveau 1
        console.log("abilityYtraining1XP - ce cursus compétence n'a pas d'investissement, on peut proposer le niveau 1 : ", l_abilityCursus.abilityKey.nom)
        l_upgradeProposals.value.push({abilityKey : l_abilityCursus.abilityKey, newLevel : 1})
      }
      else
      {
        // ca doit être un tableau de 1 element
        console.log("abilityYtraining1XP - ce cursus compétence a dejà un investissement : ", l_abilityFoundInSkillcurrentLevel)
      }
    }
    else{console.log("abilityYtraining1XP - ce cursus n'est pas une compétence, c'est ", l_abilityCursus.abilityKey.type,", on zape ")}

  }
  console.log("abilityYtraining1XP - fin de la recherche, on va proposer : ",l_upgradeProposals.value)
}

// liste des propositions à faire pour utiliser les XPs

// au montage on build la liste des propositions de formation
onMounted(() => {updateUpgradeProposalList()})


</script>
<template>
    <!-- affichage des formations deja acquise, par XP-->
    <ul>
          <li v-for="unitXpUsage in member.memberInfos.xpUsage" v-bind:key="unitXpUsage.id">
            <span v-if="unitXpUsage.xpUsed">XP utilisé</span>
            <span v-else>Xp non utilisé : choisissez un entrainement
              <select name="spendXp" id="spendXP">
                <option v-for="proposal in l_upgradeProposals" :key="proposal.abilityKey.nom" value="{{ proposal.abilityKey.nom }}">{{proposal.abilityKey.nom}}, niveau {{proposal.newLevel}}</option>
              </select>
              <button @click="learncursus(unitXpUsage.id)">Apprendre</button>
            </span>
          </li>
    </ul>
    <!-- <div>propositions : <ul>
          <li v-for="proposal in l_upgradeProposals" :key="proposal.abilityKey.nom" >
            {{proposal.abilityKey.nom}} niveau {{proposal.newLevel}}
          </li>
        </ul>>
    </div> -->

 </template>
