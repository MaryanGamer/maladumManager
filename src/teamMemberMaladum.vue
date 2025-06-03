<script setup>
import { ref, computed} from 'vue'
import abilityTraining from './abilityTraining.vue'
import abilityMaladumViewer from './abilityMaladumViewer.vue'


const member = defineModel()

const toShowMemberDetails = ref(false)
function showMemberDetails() {
  toShowMemberDetails.value = !toShowMemberDetails.value
}

//on affiche tout le temps
//const toShowMemberCaracs = ref(false)
//function showMemberCaracs() {
//  toShowMemberCaracs.value = !toShowMemberCaracs.value
//}

const toShowMemberTraining = ref(false)
function showMemberTraining() {
  toShowMemberTraining.value = !toShowMemberTraining.value
}

const toShowMemberPowers = ref(false)
function showMemberPowers() {
  toShowMemberPowers.value = !toShowMemberPowers.value
}

const memberGoldValue = computed(() => {
  return parseInt(member.value.candidate.availCompanion.Cost) + ( (parseInt(member.value.memberInfos.currentRank) -1) * 10) + parseInt(member.value.memberInfos.equipmentOtherValue)
})

function update_rank() {
  //construit le tableau des différents niveaux
  member.value.memberInfos.currentRank = 1
  var l_tab=member.value.candidate.availCompanion.XPs.split('/')
  var l_tabL=l_tab.length
  var XPseuil=0
  for (let pas = 1; pas < l_tabL; pas++) {
    XPseuil += parseInt(l_tab[pas])
    if (member.value.memberInfos.XPUsed > XPseuil ) {member.value.memberInfos.currentRank = pas+1}
  }
  member.value.memberInfos.currentRank = Math.min(member.value.memberInfos.currentRank,5)

  // À chaque éxécution, la variable "pas" augmentera de 1
  // Lorsque'elle sera arrivée à 5, le boucle se terminera.
  console.log("rank calculé : " + member.value.memberInfos.currentRank )
}

function update_life(u, what) {
  if (what == 'max')
  { member.value.memberInfos.lifeMax = parseInt(member.value.memberInfos.lifeMax) + u  }
  else
  {
    member.value.memberInfos.lifeCurrent = parseInt(member.value.memberInfos.lifeCurrent) + u
    if (member.value.memberInfos.lifeCurrent < 0) {member.value.memberInfos.lifeCurrent = 0}
    if (member.value.memberInfos.lifeCurrent > member.value.memberInfos.lifeMax) {member.value.memberInfos.lifeCurrent = member.value.memberInfos.lifeMax}
  }
}

function update_talents(u, what) {
  if (what == 'max')
  { member.value.memberInfos.talentMax = parseInt(member.value.memberInfos.talentMax) + u  }
  else
  {
    member.value.memberInfos.talentCurrent = parseInt(member.value.memberInfos.talentCurrent) + u
    if (member.value.memberInfos.talentCurrent < 0) {member.value.memberInfos.talentCurrent = 0}
    if (member.value.memberInfos.talentCurrent > member.value.memberInfos.talentMax) {member.value.memberInfos.talentCurrent = member.value.memberInfos.talentMax}
  }
}

function update_magic(u, what) {
  if (what == 'max')
  { member.value.memberInfos.magicMax = parseInt(member.value.memberInfos.magicMax) + u  }
  else
  {
    member.value.memberInfos.magicCurrent = parseInt(member.value.memberInfos.magicCurrent) + u
    if (member.value.memberInfos.magicCurrent < 0) {member.value.memberInfos.magicCurrent = 0}
    if (member.value.memberInfos.magicCurrent > member.value.memberInfos.magicMax) {member.value.memberInfos.magicCurrent = member.value.memberInfos.magicMax}
  }
}

function update_XP(u, what) {
  if (what == 'total')
  {
    //let oldMaxXP = parseInt(member.value.memberInfos.XPTotal)
    member.value.memberInfos.XPTotal = parseInt(member.value.memberInfos.XPTotal) + u
    // si on est sous le nombre d'XPs dépensés, on réajuste
    if (member.value.memberInfos.XPUsed > member.value.memberInfos.XPTotal) {member.value.memberInfos.XPTotal = member.value.memberInfos.XPUsed}
    // il ne peut pas aller au dela du max d'XPs.
    var l_tab=member.value.candidate.availCompanion.XPs.split('/')
    var l_tabL=l_tab.length
    var XPseuil=0
    for (let pas = 1; pas < l_tabL; pas++) {
        XPseuil += parseInt(l_tab[pas])
    }
    if (member.value.memberInfos.XPTotal> XPseuil) {member.value.memberInfos.XPTotal = XPseuil}

    // boucle sur tous les XPs ajoutés, pour alimenter les XPUsage    - si U positif
    if (u>0)
    {
      // variable pour récuper l'ID max dans le tableau des XPs
      //var l_temp = Array
      //l_temp = member.value.memberInfos.xpUsage
      //console.log("teamMemberMaladum update_XP, l_temp avec XPUsage : ",l_temp)
      //var l_temp2
      //l_temp2 = member.value.memberInfos.xpUsage
      //console.log("teamMemberMaladum update_XP, l_temp2 avec XPUsage : ",l_temp2)
      //l_temp = member.value.memberInfos.xpUsage.map(item => item.id)
      //console.log("teamMemberMaladum xpUsage, l_temp avec map : ",l_temp)

      var maxXPUsageId = Math.max.apply(null, member.value.memberInfos.xpUsage.map(item => item.id));
      console.log("teamMemberMaladum update_XP, maxXPUsageId : ",maxXPUsageId)
      for (let pas = 0; pas < u; pas++)
      {
        // ajout d'une entrée d'entrainement
        // plus besoin
        //member.value.memberInfos.xpUsage.push ({"id": maxXPUsageId+1+pas, "xpUsed":false})
      }
      console.log("teamMemberMaladum update_XP, après ajout des entrées dans XOPUsage : ",member.value.memberInfos.xpUsage)
    }

  }
  if (what == 'used')
  {


    member.value.memberInfos.XPUsed = parseInt(member.value.memberInfos.XPUsed) + u
    // si on dépasse les XPs totaux, faut pas le faire
    if (member.value.memberInfos.XPUsed > member.value.memberInfos.XPTotal) {member.value.memberInfos.XPUsed = member.value.memberInfos.XPTotal}
    // on ajuste le rank
    update_rank()
  }
}
</script>

<template>
  <!-- <div class="pure-u-1" >   <br/> </div>-->
<div class="pure-g global-member" >
  <div class="pure-u-1-3">
      <b><button @click="showMemberDetails">{{ toShowMemberDetails ? '-' : '+' }}</button> {{ member.candidate.availCompanion.Nom }} </b>
      - {{ member.candidate.classe.nom }} -
      Rang {{ member.memberInfos.currentRank }}
  </div>
  <div class="pure-u-1-3 alignGlobal">
      Valeur équipement divers :  <input v-model="member.memberInfos.equipmentOtherValue" /> Gs
  </div>
  <div class="pure-u-1-3 alignGlobal">
      Valeur Personnage : {{ memberGoldValue }} Gs
  </div>

  <div class="pure-u-1 " v-if="toShowMemberDetails">
    <div class="pure-g" >

      <div class="pure-u-1-4 alignGlobal" >
        <div>Santé</div>
      </div>
      <div class="pure-u-1-4 alignGlobal" >        <div>Talents</div></div>
      <div class="pure-u-1-4 alignGlobal" >        <div>Magie</div></div>
      <div class="pure-u-1-4 alignGlobal" >        <div>XPs</div></div>

      <div class="pure-u-1-8 alignGlobal" ><div>Actuelle</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Maximum</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Actuels</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Maximum</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Actuelle</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Maximum</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Acquis</div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>Utilisés</div></div>

      <div class="pure-u-1-8 alignGlobal" ><div>
        <button @click="update_life(-1,'current')">-1</button> {{ member.memberInfos.lifeCurrent }} <button @click="update_life(+1,'current')"> +1 </button>
      </div></div>
      <div class="pure-u-1-8 alignGlobal" ><div>{{ member.memberInfos.lifeMax }} <button @click="update_life(+1,'max')">+1</button></div>
      </div>
      <div class="pure-u-1-8 alignGlobal" >
        <div><button @click="update_talents(-1,'current')">-1</button>
           {{ member.memberInfos.talentCurrent }}
           <button @click="update_talents(+1,'current')"> +1 </button>
        </div>
      </div>
      <div class="pure-u-1-8 alignGlobal" ><div>{{ member.memberInfos.talentMax }} <button @click="update_talents(+1,'max')">+1</button></div>
      </div>
      <div class="pure-u-1-8 alignGlobal" ><div><button @click="update_magic(-1,'current')">-1</button> {{ member.memberInfos.magicCurrent }} <button @click="update_magic(+1,'current')"> +1 </button></div>
      </div>
      <div class="pure-u-1-8 alignGlobal" ><div>{{ member.memberInfos.magicMax }} <button @click="update_magic(+1,'max')">+1</button></div>
      </div>
      <div class="pure-u-1-8 alignGlobal" ><div><button @click="update_XP(-1,'total')">-1</button> {{ member.memberInfos.XPTotal }} <button @click="update_XP(+1,'total')"> +1 </button></div>
      </div>
      <div class="pure-u-1-8 alignGlobal" ><div>{{ member.memberInfos.XPUsed }}</div>
      </div>

      <div class="pure-u-1" >
        <br/>
      </div>
      <div id="training" class="pure-u-1" >
        <div class="pure-g global-training" >
          <div class="pure-u-1" >
            <button @click="showMemberTraining">{{ toShowMemberTraining ? '-' : '+' }}</button> Training
            <span v-if="member.memberInfos.XPUsed < member.memberInfos.XPTotal"> (Vous avez des XPs non utilisé)</span>
          </div>
          <div v-if="toShowMemberTraining" class="pure-u-1">
            <abilityTraining v-model="member" @response="(xpUsedVariation) => update_XP(xpUsedVariation, 'used')"  />
          </div>
        </div>
      </div>
      <div class="pure-u-1" ><br/></div>
      <div id="powers" class="pure-u-1" >
        <div class="pure-g global-powers" >
          <div class="pure-u-1" >
            <button @click="showMemberPowers">
            {{ toShowMemberPowers ? '-' : '+' }}</button> Pouvoirs
          </div>

          <div v-if="toShowMemberPowers" class="pure-u-1">
            <ul>
              <li v-for="acquiredAbility in member.memberInfos.allAcquiredAbilities" v-bind:key="acquiredAbility.id">
                <span class=tooltip>
                  {{  acquiredAbility.abilityKey.type }} - {{  acquiredAbility.abilityKey.nom }} - Niveau {{  acquiredAbility.acquiredLevel }}
                <abilityMaladumViewer :abilityKeyNom="acquiredAbility.abilityKey.nom"  :abilityKeyType="acquiredAbility.abilityKey.type" :tooltipOnLeft="false" />
              </span>

              </li>
            </ul>
          </div>
        </div>

      </div>

    </div>
  </div>
</div>

 </template>
