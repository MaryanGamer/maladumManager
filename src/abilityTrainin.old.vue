<script setup>
import { ref,onMounted } from 'vue'
const emit = defineEmits(['response'])

// voir abilityaladum.vue pour le format des objets
// on récupère un membre, et on va lui proposer des formations, selon ses XPs libre et sa formation acquise

// on doit récupérer le membre en question.
const member = defineModel()
// on remplit son usage d'XP par defaut, si c'est pas fait
let l_xpUsage = Array
// compteur d'ID des XPUsage, pour avoir un bon ID à ajouter
// est à mettre à jour à chaque relistage des XPUsages
var l_XPUsageMaxID = 0

// pour récupérer le choix, faisons un tableau de 30 element. Chaque élément sera le choix d'achat d'XP choisi
const l_tabChoicesSelected =ref ([30])

// alimentation par défaut
function initXpUsage ()
{
  l_xpUsage=member.value.memberInfos.xpUsage
  // boucle d'alimentation si il est vide
  // si il y a déjà des éléments, on s'assure qu'il y a en a suffisemment, par rapport aux XP acquis.
  for (let pas = 0; pas < parseInt(member.value.memberInfos.XPTotal); pas++) {
    // tant qu'on est dan s le tableau des XPUsage, on ne fait rien (mais on check le maxID)
    // au delà, on ajoute les possibilités d'utiliser des XPs
    if (pas > l_xpUsage.length)
    {
      l_XPUsageMaxID++
      member.value.memberInfos.xpUsage.push ({"id": l_XPUsageMaxID, "xpUsed":false})
      console.log("initXpUsage - pas = ",pas," - ajout element par defaut avec l_XPUsageMaxID : ",l_XPUsageMaxID)
    }
    else
    {
      // pas est encore dans la plage des XPUsage existants.
      //on considère le Max
      console.log("initXpUsage - pas = ",pas," - Unité xpUsage existe déjà avec id : ",l_xpUsage[pas].id)
      if (member.value.memberInfos.xpUsage[pas].id > l_XPUsageMaxID) {l_XPUsageMaxID=member.value.memberInfos.xpUsage[pas].id}
    }

    //alimentation par défaut du choix d evolution dans le tableau
  }

  console.log("initXpUsage - abilityTraining, xpUsage : ",member.value.memberInfos.xpUsage)
  console.log("initXpUsage - maxID : ",l_XPUsageMaxID)
}

// format : tableau de  {"abilityKey" :  { "nom":"Plonger à couvert","type":"Compétence"  },newLevel : "1"}
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
    //console.log("check cursus : ",l_abilityCursus)
    // scan skillCurrentLevel si on trouve la compétence (et si c'est une compétence.)
    if (l_abilityCursus.abilityKey.type == "Compétence")
    {
      l_abilityFoundInSkillcurrentLevel = null
      //console.log("updateUpgradeProposalList - on va chercher dans ",member.value.memberInfos.allAcquiredAbilities)
      //console.log("updateUpgradeProposalList - trouve-t-on dans les pouvoirs connus ? ",l_abilityCursus.abilityKey)
      l_abilityFoundInSkillcurrentLevel = member.value.memberInfos.allAcquiredAbilities.filter((t) => t.abilityKey == l_abilityCursus.abilityKey)
      if (l_abilityFoundInSkillcurrentLevel.length == 0)
      {
        // rien n'a été investi sur cette compétence. on peut proposer le niveau 1
        l_upgradeProposals.value.push({abilityKey : l_abilityCursus.abilityKey, newLevel : 1})
      }
      else
      {
        // ca doit être un tableau de 1 element
        //console.log("updateUpgradeProposalList - ce cursus compétence a dejà un investissement : ", l_abilityFoundInSkillcurrentLevel)
        // comparaison des niveaux vs le max possible
        let l_current = parseInt(l_abilityFoundInSkillcurrentLevel[0].acquiredLevel)
        //console.log("updateUpgradeProposalList - déjà acquis au niveau  : ", l_current)
        //console.log("updateUpgradeProposalList - déjà acquis au niveau  : ", l_abilityFoundInSkillcurrentLevel[0].acquiredLevel)

        let l_singleIncrease = {abilityKey : l_abilityCursus.abilityKey, newLevel : l_current+1}
        // on propose niveau supplémentaire ?
        if (l_current+1 > 3) {
            //console.log("updateUpgradeProposalList - on propose pas d'investissement : ", l_singleIncrease)
        }
        else {
          l_upgradeProposals.value.push(l_singleIncrease)
          //console.log("updateUpgradeProposalList - on propose un investissement : ", l_singleIncrease)
        }
      }
    }
    else{console.log("updateUpgradeProposalList - ce cursus n'est pas une compétence, c'est ", l_abilityCursus.abilityKey.type,", on zape ")}
  }
  console.log("updateUpgradeProposalList - fin de la recherche des choix, on va proposer : ",l_upgradeProposals.value)

  // alimentation tu tableau des choix par défaut.
  for (let pas = 0; pas < member.value.memberInfos.xpUsage.length; pas++) {
    // sur chaque choix, on met la valeur par defaut sutr le 1er choix
    l_tabChoicesSelected.value[pas] = l_upgradeProposals.value[0]
  }
  //console.log("updateUpgradeProposalList - fin des selections pr defaut : ",l_tabChoicesSelected.value)

}

function learnCursus(XPId){

  // XPId indique quel XPUsage on modifie.
  console.log("learnCursus - XPUsage.ID utilisé : ",XPId )
  // le l_tabChoicesSelected liste les choix des différentes combos
  console.log("learnCursus - Tableau des selections dans les listes de choix : ",l_tabChoicesSelected.value)
  let l_increaseSelection = l_tabChoicesSelected.value[XPId]
  console.log("learnCursus - a été choisi cette amélioration : ",l_increaseSelection)

  // il faut :
  // #1 mettre à jour la liste des abilities

  // id de la nouvelle entrée dans XPUsage, on prend l'ID max qu'on augmente
  l_XPUsageMaxID++
  // nouvel ID de Acquired Ability
  var l_acquiredAbilityMaxID =0
  if (member.value.memberInfos.allAcquiredAbilities.length > 0)
  {
    l_acquiredAbilityMaxID= Math.max.apply(null, member.value.memberInfos.allAcquiredAbilities.map(item => item.id));
  }
  l_acquiredAbilityMaxID ++
  console.log("learnCursus - futur index XPUsage : ",l_XPUsageMaxID)
  console.log("learnCursus - futur index acquiredAbility : ",l_acquiredAbilityMaxID)

  // objet qui heberge l'information de niveau
  let l_abilityAcquired = Object
  l_abilityAcquired = {id:l_acquiredAbilityMaxID, abilityKey : l_increaseSelection.abilityKey,acquiredLevel:l_increaseSelection.newLevel}
  console.log("learnCursus - l_abilityAcquired : ",l_abilityAcquired)
  // object temporaire de liste des abilités du personnage
  let l_abilitiesAcquiredTemp = Object

  console.log("allAcquiredAbilities avant MAJ : ",member.value.memberInfos.allAcquiredAbilities) // résultat de log bizarre
  // si le nouveau niveau est 1, on ajoute cela à la liste des skillCurrentLevels
  if (parseInt(l_increaseSelection.newLevel)==1)
  {
    // on ajoute simplement l'ability à la liste
    member.value.memberInfos.allAcquiredAbilities.push(l_abilityAcquired)
  }
  else
  {
    //on cherche donc la compétence qui augmente
    // on va l'exclure et injecter la nouvelle
    // liste temporaire
    l_abilitiesAcquiredTemp = null
    l_abilitiesAcquiredTemp = member.value.memberInfos.allAcquiredAbilities.filter((t) => t.abilityKey != l_increaseSelection.abilityKey)
    l_abilitiesAcquiredTemp.push(l_abilityAcquired)
    member.value.memberInfos.allAcquiredAbilities=l_abilitiesAcquiredTemp
  }
  console.log("allAcquiredAbilities après MAJ : ",member.value.memberInfos.allAcquiredAbilities)

  //#2 : tracer l'utilisation de l'XP
  console.log("xpUsage avant MAJ : ",member.value.memberInfos.xpUsage)
  var l_xpUsage = member.value.memberInfos.xpUsage.filter((t) => t.id != XPId)
  //l_xpUsageUpdate = member.value.memberInfos.xpUsage.filter((t) => t.id == XPId)
  //l_xpUsageUpdate
  member.value.memberInfos.xpUsage=l_xpUsage
  member.value.memberInfos.xpUsage.push ({id:XPId, xpUsed : true, acquiredAbility :l_abilityAcquired})
  console.log("xpUsage après MAJ : ",member.value.memberInfos.xpUsage)

  // #4 Indiquer qu'un XP a été utilisé
  //member.value.memberInfos.XPUsed ++
  emit('response', 1)

  // #3 : remettre à plat les propositions d'utilisation des XPs
  initXpUsage()
  updateUpgradeProposalList()

}



function forgetCursus(XPId){
  // on supprime l'apprentissage
  // XPId indique quel XP on modifie.
  console.log("forgetCursus - XP ID utilisé : ",XPId )
  // quel cursus veut on supprimer ?
  console.log("forgetCursus - allAcquiredAbilities avant forget : ",member.value.memberInfos.allAcquiredAbilities)
// Attnrtion, l_unitXpUsageToFree tableau de taille 1
  var l_unitXpUsageToFree = member.value.memberInfos.xpUsage.filter((t) => t.id == XPId)
  console.log("forgetCursus - Cursus à libérer avant forget : ",l_unitXpUsageToFree[0])
  var l_abilityKeyToFree=l_unitXpUsageToFree[0].acquiredAbility.abilityKey
  console.log("forgetCursus - abilityKey à libérer : ",l_abilityKeyToFree)


  // est ce qu'on peut libérer cette ligne d'XPs ?
  //le trait qui est tenté doit être le niveau le plus élevé, aprmi tous les XPs utilisés.
  // on prend la clef de l'abilité qu'on veut retirer, et on vérifie que le niveaui demandé à supprimer est bien le pus grand.
  var l_cursusAcquiredLeveltoFree = l_unitXpUsageToFree[0].acquiredAbility.acquiredLevel
  var l_tabXPUsed =  member.value.memberInfos.xpUsage.filter((t) => t.xpUsed)
  var l_maxAcquiredForThisAbility = Math.max.apply(null, l_tabXPUsed.map(item => item.acquiredAbility.acquiredLevel));
  console.log("forgetCursus - comparaison entre le niveau qu'on veut retirer : ",l_cursusAcquiredLeveltoFree, " et le niveau maximum acquis : ",l_maxAcquiredForThisAbility)
  if (l_maxAcquiredForThisAbility > l_cursusAcquiredLeveltoFree)
  {
    // on essaie pas de supprimer le niveau le plus elevé. donc on refuse.
    var l_msg = "Vous cherchez à retirer l'apprentissage du niveau "
    l_msg = l_msg.concat(l_cursusAcquiredLeveltoFree," alors qu'il existe un niveau ",l_maxAcquiredForThisAbility,", Suppression interdite")
    alert(l_msg)
  }
  else{

    // on peut libérer l'XP
    // retirer le niveau des compétences acquises.
    // Attention, l_TabAcquiredAbility est un tableau de taille 1
    var l_TabAcquiredAbility = member.value.memberInfos.allAcquiredAbilities.filter((t) => t.abilityKey == l_abilityKeyToFree)
    console.log("forgetCursus - l_TabAcquiredAbility : ",l_TabAcquiredAbility)
    var l_acquiredAbility = l_TabAcquiredAbility[0]
    console.log("forgetCursus - l_acquiredAbility : ",l_acquiredAbility)
    var l_newAcquiredAbilities = member.value.memberInfos.allAcquiredAbilities.filter((t) => t.abilityKey != l_abilityKeyToFree)
    console.log("forgetCursus - l_newAcquiredAbilities : ",l_newAcquiredAbilities)
    if (parseInt(l_acquiredAbility.acquiredLevel)==1)
    {
      // suppression de l'entrée déjà faite, rien à faire
    }
    else{
      // diminution du niveau.
      l_acquiredAbility.acquiredLevel --
      l_newAcquiredAbilities.push(l_acquiredAbility)
    }
    member.value.memberInfos.allAcquiredAbilities = l_newAcquiredAbilities
    console.log("forgetCursus - allAcquiredAbilities après MAJ : ",member.value.memberInfos.allAcquiredAbilities)
    // Reconstruction de la liste des XPs utilisés
    var l_XPUsageUpdated = member.value.memberInfos.xpUsage.filter((t) => t.id != XPId)
    l_XPUsageUpdated.push({id:XPId, xpUsed : false})
    member.value.memberInfos.xpUsage=l_XPUsageUpdated
    console.log("forgetCursus - xpUsage après MAJ : ",member.value.memberInfos.xpUsage)

    // MaJ du nombre d'XPs utilisés
    //member.value.memberInfos.XPUsed --
    emit('response', -1)

    // remettre à plat les propositions d'utilisation des XPs
    initXpUsage()
    updateUpgradeProposalList()


  }



}

  // au montage on build la liste des propositions de formation
  onMounted(() => {initXpUsage();updateUpgradeProposalList()})


</script>
<template>
    <!-- affichage des formations deja acquise, par XP-->
    <ul>
          <li v-for="unitXpUsage in member.memberInfos.xpUsage" v-bind:key="unitXpUsage.id">
            <span v-if="unitXpUsage.xpUsed">XP ({{ unitXpUsage.id }}) utilisé ({{unitXpUsage.acquiredAbility.abilityKey.nom}} niveau  : {{unitXpUsage.acquiredAbility.acquiredLevel}})
              <button @click="forgetCursus(unitXpUsage.id)">X</button>
            </span>
            <span v-else>Xp ({{ unitXpUsage.id }}) non utilisé : choisissez un entrainement
              <select v-model="l_tabChoicesSelected[unitXpUsage.id]" name="'spendXP'.concat(unitXpUsage.id)"
              id="'spendXP'.concat(unitXpUsage.id)">
                <option v-for="proposal in l_upgradeProposals" :key="proposal.abilityKey.nom" :value="proposal">{{proposal.abilityKey.nom}}, niveau {{proposal.newLevel}}</option>
              </select>
              <button @click="learnCursus(unitXpUsage.id)">Apprendre</button>
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
