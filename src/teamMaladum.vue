<script setup>
import { ref} from 'vue'
import teamInfoTeamMaladum from './teamInfoTeamMaladum.vue'
import teamMembersMaladum from './teamMembersMaladum.vue'
import teamAddMemberMaladum from './teamAddMemberMaladum.vue'
//import abilityMaladum from './abilityMaladum.vue'

// tableau du référentiel des abilités
//const abilityReferential = ref()
//provide(/* key */ 'abilityReferential', /* value */ abilityReferential)

// Objet géré ici : l'equipe de personnages
// l'ensemble de la partie est géré dans gameMaladum

//const maladumGame = ref({campaign : {}})
const team = defineModel()
//const team = ref ({teamName : "",members : []})

function integrateCandidate(candidate) {

  //console.log ('referentiel des abilités : ',abilityReferential.value)
  //console.log('candidat à intégrer dans team : ',candidate)
  //console.log('candidat companion à intégrer dans team : ',candidate.availCompanion)
  console.log('classe du candidat : ',candidate.classe)

  // variables de définition d'un nouveau membre, par dégfaut.
  // object candidate qui contient
  let l_candidat = new Object()
  //    object availCompanion
  //    object classe
  // object memberInfos qui contient
  let l_memberInfos = new Object()
  //    XPTotal
  let l_XPTotal = 0
  //    XPUsed
  let l_XPUsed = 0
  //    currentRank
  let l_currentRank = 1
  //  tableau avec liste des utilisations d'XPs : used (boolean) - ability selectioné - niveau pris (si compétence)
  let l_xpUsage = []

  // allAcquiredAbilities, c'est un tableau avec pour chaque élément :
  //  un abilityKey (voir abilityMaladum)
  //  Le niveautotal acquis
  let l_allAcquiredAbilities = []
  //    Tableau spellLearned, sorts appris, qui contient un tableau avec pour chaque élément
  //      spellName
  //      spellType
  //      spellLevel
  //              let l_spellLearned = [] finalement pas utilisé tout dans allAcquiredAbilities
  //    lifeMax
  let l_lifeMax = 0
  //    lifeCurrent
  let l_lifeCurrent = 0
  //    talentMax
  let l_talentMax = 0
  //    talentCurrent
  let l_talentCurrent = 0
  //    magicMax
  let l_magicMax = 0
  //    magicCurrent
  let l_magicCurrent = 0
  //    Tableau equipment, tableau avec pour chaque élément
  let l_equipment = []
  //      itemName
  //      itemWidth
  //      itemType
  //      itemPriceBuy
  //      itemPriceSell
  let l_member=new Object()

  l_memberInfos =  {XPTotal : l_XPTotal , XPUsed : l_XPUsed,  currentRank: l_currentRank,xpUsage : l_xpUsage, allAcquiredAbilities : l_allAcquiredAbilities,    lifeMax :  l_lifeMax,   lifeCurrent :  l_lifeCurrent ,   talentMax : l_talentMax ,    talentCurrent : l_talentCurrent ,   magicMax : l_magicMax,    magicCurrent :  l_magicCurrent,  equipment :  l_equipment , equipmentOtherValue : 0 }
  l_member = { candidate: l_candidat, memberInfos : l_memberInfos }

  // le candidate doit être ajouté à l'équipe
  l_candidat = candidate
  l_member.candidate=l_candidat
  console.log('candidate recu intégré dans l object member.')

  // setup des infos du membre memberInfos
  //    XPTotal : total XP candidat
  l_member.memberInfos.XPTotal = l_member.candidate.availCompanion.XPs[0]
  // boucle sur les XPs, pour ajouter des éléments dans le tableau des usages d'XPs
  for (let c = 0; c < l_member.memberInfos.XPTotal; c++) {
    // creation d'une entrée d'utilisation d'XPs
    // plus besoin
    // l_member.memberInfos.xpUsage.push({"id" : c, "xpUsed" : false})
  }

  //    XPUsed : 0
  l_member.memberInfos.XPUsed = 0
  //    currentRank : 1
  l_member.memberInfos.currentRank = 1
  //    Tableau skillCurrentLevels : TODO
  //    Tableau spellLearned : aucun à l'intégration du membre. tableau vide déjà fourni, on fait rien
  //    lifeMax - 5eme caractere du companion "Santé": "1/2/3/6",
  l_member.memberInfos.lifeMax = l_member.candidate.availCompanion.Life[4]
  //    lifeCurrent - début à fond
  l_member.memberInfos.lifeCurrent = l_member.memberInfos.lifeMax
  //    talentMax
  l_member.memberInfos.talentMax = l_member.candidate.availCompanion.Talent[0]
  //    talentCurrent
  l_member.memberInfos.talentCurrent = l_member.memberInfos.talentMax
  //    magicMax
  l_member.memberInfos.magicMax = l_member.candidate.availCompanion.Magie[0]
  //    magicCurrent
  l_member.memberInfos.magicCurrent = l_member.memberInfos.magicMax
  //    Tableau equipment : vide, on fait rien
  console.log('XP du candidat : ',l_candidat.availCompanion.XPs,', XP init du candidat : ',l_member.memberInfos.XPTotal)

  // ajout des pouvoirs aux acquired abilities
  var l_cpt=1
  var l_tab = Array
  var l_object = Object
  var l_toAddtoAcquired = false

  // Ajout des pouvoir du companion aux acquired abilitites
  l_member.candidate.availCompanion.aptitudes.forEach( (singleAptitude) => {
    console.log("integrateCandidate - abilité du companion en analyse : ",singleAptitude);
    l_toAddtoAcquired = false
    switch (singleAptitude.abilityKey.type) {
      case "Compétence":
        // on vérifie si compétence déjà acquise à un niveau
        if (parseInt(singleAptitude.cursusInitialLevel) >= 1 )
        {
          // à mettre dans abilités acquises
          l_object= {"id" : l_cpt , "abilityKey" : singleAptitude.abilityKey, "acquiredLevel" : singleAptitude.cursusInitialLevel}
          l_toAddtoAcquired = true
          l_cpt ++
        }
        break;
      case "Sort":
      case "Pouvoir":
        // A ajouter
        l_object= {"id" : l_cpt , "abilityKey" : singleAptitude.abilityKey, "acquiredLevel" : singleAptitude.cursusMaxLevel }
        l_toAddtoAcquired = true
        l_cpt ++
        break;
      default:
        console.warn("integrateCandidate - une abilité du companion ne peut pas être interprétée");
    }
    if (l_toAddtoAcquired)
    {
      // on ajoute
      l_member.memberInfos.allAcquiredAbilities.push(l_object)
    }

  })


  // Ajout des pouvoirs acquis de classe dans le memberInfos/l_allAcquiredAbilities
  // on va boucler sur les pouvoirs natifs (les pouvoir qui sont pas des compétences)
  l_tab = l_member.candidate.classe.aptitudes.filter((singleAptitude) => singleAptitude.abilityKey.type != "Compétence")
  // ensuite, il faut retirer les sorts, si il y a un pouvoir de type magie (car il faudra, alors, les apprendre)
  let l_tabIsMagic = Object
  l_tabIsMagic=null
  l_tabIsMagic = l_tab.filter((singleAptitude) => singleAptitude.abilityKey.type == "Magie")
  if (l_tabIsMagic.length == 0)
      {
        // pas de magie. Seulement peut être quelques sorts (acquis), on les laisse dans la liste à retourer dans les acquiredAbilities
      }
      else
      {
        // il y a de la magie, il faut donc retiurer les sorts
        console.log('integrateCandidate l_tab des pouvoirs à reporter - on retire les sorts : ',l_tab)
        l_tab = l_tab.filter((singleAptitude) => singleAptitude.abilityKey.type != "Sort")

      }

  //l_tab = l_tab.filter((singleAptitude) => singleAptitude.abilityKey.type != "Sort")
  console.log('integrateCandidate l_tab des pouvoirs de classe à reporter dans allAcquiredAbilities : ',l_tab)

  //var l_object = object
  l_tab.forEach( (singleAptitude) => {
    // creation objet
    var l_object= {"id" : l_cpt , "abilityKey" : singleAptitude.abilityKey, "acquiredLevel" : singleAptitude.cursusMaxLevel}
    l_member.memberInfos.allAcquiredAbilities.push(l_object)
    l_cpt++
  });

  team.value.members.push(l_member)

}

const toShowTeam = ref(false)
function showTeams() {
  toShowTeam.value = !toShowTeam.value
}
</script>

<template>
<div class="pure-g global-team">
  <div class="pure-u-1" > <button @click="showTeams">{{ toShowTeam ? '-' : '+' }}</button> Votre confrérie </div>
  <div v-if="toShowTeam" class="pure-u-1" >
    <div class="pure-u-1" >
      <teamInfoTeamMaladum v-model=team />
    </div>
    <div class="pure-u-1" >
      <teamMembersMaladum v-model=team.members />
    </div>
    <div class="pure-u-1" >
      <teamAddMemberMaladum @selectedCandidate="(candidate) => integrateCandidate(candidate)" />
    </div>
  </div>
</div>

 </template>
