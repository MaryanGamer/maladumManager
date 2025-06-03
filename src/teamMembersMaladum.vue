<script setup>
import { ref } from 'vue'

import teamMemberMaladum from './teamMemberMaladum.vue'

// format d'un membre de la team :
// object candidate qui contient
//    object availCompanion
//    object classe
// object memberInfos qui contient
//    XPTotal
//    XPUsed
//    memberGoldValue => ce sera un computed
//    currentRank
//    Tableau d'utilisation des XPs : xpUsage
//      "id", "xpUsed" (true/false), objet  acquiredAbility (voir abilityMaladum)
//    Tableau allAcquiredAbilities (voir abilityMaladum)
//    NON PRESENT
            //Tableau spellLearned, sorts appris, qui contient un tableau avec pour chaque élément
            //      spellName
            //      spellType
            //      spellLevel
//    lifeMax
//    lifeCurrent
//    talentMax
//    talentCurrent
//    magicMax
//    magicCurrent
//    equipmentOtherValue : indique une valeur global d'équipement du personnage. c'est donc une valeur d'or ajoutée et gérée par l'utilisateur
//    equipmentDetail : Tableau avec pour chaque élément
//      itemName
//      itemWidth
//      itemType
//      itemPriceBuy
//      itemPriceSell

const members = defineModel()
//const l_members = defineProps({members : Array})

function removeMember(memberToDelete) {
  members.value = members.value.filter((m) => m !== memberToDelete)
}


const toShowCharacters = ref(false)
function showCharacterss() {
  toShowCharacters.value = !toShowCharacters.value
}

</script>

<template>

  <div class="pure-u-1" ><button @click="showCharacterss">{{ toShowCharacters ? '-' : '+' }}</button>Vos personnages</div>
  <div v-if="toShowCharacters">
    <div class="pure-u-1 alignGlobal" v-if="members.length === 0">Pas de personnage dans votre confrérie</div>

    <div v-else v-for="(member,i) in members" :key="member.candidate.availCompanion.Nom">
      <div class="pure-u-1">
        <teamMemberMaladum v-model="members[i]" />
      </div>
      <div class="pure-u-1 alignGlobal global-member" >
          <button @click="removeMember(member)">Renvoyer {{ member.candidate.availCompanion.Nom }}</button>
      </div>

      <div class="pure-u-1" >  </div>

    </div>
  </div>


 </template>
