<script setup>
import {onMounted, ref , provide, useTemplateRef} from 'vue'
import campaignMaladum from './campaignMaladum.vue'
import teamMaladum from './teamMaladum.vue'

//import teamInfoTeamMaladum from './teamInfoTeamMaladum.vue'
//import teamMembersMaladum from './teamMembersMaladum.vue'
//import teamAddMemberMaladum from './teamAddMemberMaladum.vue'
import abilityMaladum from './abilityMaladumLoader.vue'

// tableau du référentiel des abilités et regles
const abilityReferential = ref()
provide(/* key */ 'abilityReferential', /* value */ abilityReferential)

// Objet global géré
// l'ensemble permet d'avoir une vue sur une campagne et sur les personnages.
// on a une partie : maladumGame
// dans la partie, on a :
// - un objet campagne (campaign), composé de :
//  - Nom de la campagne : campaignName
//  - Retard : campaignDelay
//  - Prochain scenario : campaignNextScenario
//  - autres infos (un blob de données : campaignOtherInfos) (un string, en fait)
// - un objet Equipe : team , composé de :
//  - Renommée : teamFame
//  - nom de l'équipe : teamName
//  - Tresor de l'équipe : teamTreasure
//  - Réserve de matériel stocké : storage et secureStorage (String)
//  - liste des membres : [members] -format détaillé en commentaires de teamMembersMaladum

let l_campaign = new Object()
l_campaign =  {campaignName : "" , campaignDelay : 0,  campaignNextScenario : "", campaignOtherInfos : ""}
let l_team = new Object()
l_team =  {teamName : "", teamFame : 0 , teamTreasure : 0, members : [], storage : "", secureStorage : ""}

const maladumGame = ref({campaign : l_campaign , team : l_team })
//const team = ref ({teamName : "",members : []})

function downLoadCurrentGame(exportObj, exportName){
    var dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(exportObj, null, 2));
    // JSON.stringify(exportObj, null, 2)
    var downloadAnchorNode = document.createElement('a');
    var exportNameTrim = exportName.trim()
    if (exportNameTrim == "") {exportNameTrim='gameMaladum'}

    downloadAnchorNode.setAttribute("href",     dataStr);
    downloadAnchorNode.setAttribute("download", exportNameTrim + ".json");
    document.body.appendChild(downloadAnchorNode); // required for firefox
    downloadAnchorNode.click();
    downloadAnchorNode.remove();
  }

const l_elt = useTemplateRef('gameImport')

function chooseGameImport () {
  //this.element.click()
  //const l_elt = useTemplateRef('teamImport')
  l_elt.value.click()
}

function importGame (event) {
  const files = event.target.files
  if (files.length <= 0) {
    return false;
  }

  var fr = new FileReader();
  fr.onload = function(e) {
    console.log(e);
    var result = JSON.parse(e.target.result);
    //var formatted = JSON.stringify(result, null, 0);
		maladumGame.value = result;
  }

  fr.readAsText(files.item(0));

  //let filename = files[0].name
  //const fileReader = new FileReader()
  //fileReader.addEventListener('load', () => {
  //  this.imageUrl = fileReader.result
  //})
  //fileReader.readAsDataURL(files[0])
  //this.image = files[0]
}

onMounted(() => {console.log("gameMaladum mounted, abilities referential = ",abilityReferential.value )})

</script>

<template>
  <div class="pure-g global-game">
    <div class="pure-u-1"><abilityMaladum @listAllAbilities="(liste) =>
    {
      abilityReferential = liste
      console.log('gameMaladum receives abilities, abilities referential = ',abilityReferential)
    }"/></div>

    <div class="pure-u-1 pure-u-sm-1-3 alignGlobal">
      <button class="btn btn-info" @click="chooseGameImport">Importer une partie</button>
      <input
      type="file"
      style="display: none"
      ref="gameImport"
      @change="importGame"/>
    </div>
    <div class="pure-u-1 pure-u-sm-1-3 alignGlobal"> Votre Partie en cours </div>
    <div class=" pure-u-1 pure-u-sm-1-3 alignGlobal"><button @click="downLoadCurrentGame(maladumGame,maladumGame.team.teamName)">Exporter la partie</button> </div>

    <div class="pure-u-1-1">
      <campaignMaladum v-model=maladumGame.campaign />
    </div>
    <div class="pure-u-1-1">
      <teamMaladum v-model=maladumGame.team />
    </div>


    <!--
      <button @click="upLoadTeam(members,'maladumteam')">team à importer</button>
      <input type="file" id="selectFiles" value="Import" /><button id="import">Importer</button>
      -->
    </div>
 </template>
