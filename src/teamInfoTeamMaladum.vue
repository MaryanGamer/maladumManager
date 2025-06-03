<script setup>
import {computed, ref} from 'vue'

//import abilityTraining from './abilityTraining.vue'
// Renommée : teamFame
//  - nom de l'équipe : teamName
//  - Tresor de l'équipe : teamTreasure
//  - liste des membres : [members] -format détaillé en commentaires de teamMembersMaladum

const team = defineModel()

const l_treasureVariation = ref(0)

const teamGoldValue = computed(() => {
  let l_value = 0
  team.value.members.forEach((member) =>
    l_value += parseInt(member.candidate.availCompanion.Cost) + ( (parseInt(member.memberInfos.currentRank) -1) * 10) +  parseInt(member.memberInfos.equipmentOtherValue)
    )
  return l_value
})

function updateFame(u) {
  team.value.teamFame = parseInt(team.value.teamFame) + u
  if (team.value.teamFame < 0) {team.value.teamFame = 0}
  if (team.value.teamFame > 50) {team.value.teamFame = 50}

}
function updateTreasure() {
  team.value.teamTreasure = parseInt(team.value.teamTreasure) + l_treasureVariation.value
  if (team.value.teamTreasure < 0) {team.value.teamTreasure = 0}
  if (team.value.teamTreasure > 5000) {team.value.teamTreasure = 5000}
  l_treasureVariation.value = 0

}
function updateTreasureVariation(u) {
  l_treasureVariation.value +=  u

}

const encaisseOuDebite = computed(() => {
  if (l_treasureVariation.value > 0)
    { return "Encaisser"}
  else
    { return "Débiter" }
 })

</script>

<template>

<div  class="pure-g global-team-info">

  <div class="pure-u-1-2 pure-u-sm-1-2 pure-u-md-1-4">
    <div  class="pure-g ">
      <div class="pure-u-1 alignGlobal">
        <div>nom de la Confrérie</div>
      </div>
      <div class="pure-u-1 alignGlobal">
        <div>
          <input v-model="team.teamName" placeholder="Soignez votre réputation" /> {{ team.teamName }}
        </div>
      </div>
    </div>
  </div>

  <div class="pure-u-1 pure-u-sm-1-2 pure-u-md-1-4">
    <div  class="pure-g ">
      <div class="pure-u-1 alignGlobal">
        <div>Valeur</div>
      </div>
      <div class="pure-u-1 alignGlobal">
        <div>
          {{ teamGoldValue }} Gs
        </div>
      </div>
    </div>
  </div>
  <div class="pure-u-1 pure-u-sm-1-2 pure-u-md-1-4">
    <div  class="pure-g ">
      <div class="pure-u-1 alignGlobal">
        <div>Renommée</div>
      </div>
      <div class="pure-u-1 alignGlobal">
        <div>
          <button @click="updateFame(-1)">-</button> {{ team.teamFame }} <button @click="updateFame(+1)">+</button>
        </div>
      </div>
    </div>

  </div>
  <div class="pure-u-1 pure-u-sm-1-2 pure-u-md-1-4 alignGlobal">
    <div class="pure-g">
      <div class="pure-u-1 alignGlobal">
        <div> Richesses  {{ team.teamTreasure }} Gs
        </div>
      </div>
      <div class="pure-u-1 alignGlobal">

        <button @click="updateTreasureVariation(-10)">--</button><button @click="updateTreasureVariation(-1)">-</button>
        <button @click="updateTreasure()">{{ encaisseOuDebite }} {{ l_treasureVariation }} Gs</button>
        <button @click="updateTreasureVariation(+1)">+</button><button @click="updateTreasureVariation(+10)">++</button>

      </div>
    </div>
  </div>
  <div class="pure-u-1 pure-u-sm-1-2 alignGlobal">
    <div>Equipement <br/>stocké </div>
    <div> <textarea id="storage" v-model="team.storage"> </textarea>
    </div>
  </div>
  <div class="pure-u-1 pure-u-sm-1-2 alignGlobal">
    <div> <br/>sécurisé </div>
    <div> <textarea id="storage" v-model="team.secureStorage"> </textarea>
    </div>
  </div>

</div>


</template>
<style>


</style>
