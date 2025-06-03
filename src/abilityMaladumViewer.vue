 <script setup>
import {  inject } from 'vue'

const props = defineProps({
  abilityKeyNom: String ,
  abilityKeyType : String ,
  tooltipOnLeft : Boolean
})

// referentiel des abilités, instancié par ailleurs
const abilityReferentiel = inject('abilityReferential')

// un filtre sur l'abilité en argument entrant
//console.log("abilityViewer - abilityReferentiel = ",abilityReferentiel.value)
console.log("abilityViewer - abilityKeyNom /  = ",props.abilityKeyNom, "/",props.abilityKeyType)

var filteredAbility = Array
var textTooltip = String
textTooltip = "<center>" + props.abilityKeyType + " <i>" + props.abilityKeyNom + "</i> : </center><br/>"

filteredAbility = abilityReferentiel.value.filter((t) => t.abilityKey.nom == props.abilityKeyNom && t.abilityKey.type == props.abilityKeyType )
console.log("abilityMaladumViewer, donnee filtrée : ",filteredAbility)
if (filteredAbility.length > 0)
{
  //console.log("abilityMaladumViewer, donnee filtrée taille : ",filteredAbility.length)
  // si c'est un type compétence, on devrait avoir un accès à un tableau abilityDetail.descriptionNiveaux
  if (filteredAbility[0].abilityKey.type == "Compétence")
  {
    console.log("abilityMaladumViewer, donnee filtrée descriptionNiveaux : ",filteredAbility[0].abilityDetail.descriptionNiveaux)
    if (Object.hasOwn(filteredAbility[0].abilityDetail,"descriptionNiveaux"))
    {
      console.log("abilityMaladumViewer, compétence avec objet descriptionNiveaux ")
      // scan du tableau
      for (let step = 0; step < filteredAbility[0].abilityDetail.descriptionNiveaux.length; step++) {
        console.log("abilityMaladumViewer - descriptionNiveaux ",step," : ",filteredAbility[0].abilityDetail.descriptionNiveaux[step]);
        textTooltip = textTooltip+ " " + filteredAbility[0].abilityDetail.descriptionNiveaux[step]
      }

    }
    else
    {
      console.log("abilityMaladumViewer, compétence SANS objet descriptionNiveaux - on affiche rien dans le tootip ")
    }
  }
  else
  {
    // on va chercher le champ abilityDetail/description
    console.log("abilityMaladumViewer, donnee filtrée description : ",filteredAbility[0].abilityDetail.description)
    if (Object.hasOwn(filteredAbility[0].abilityDetail,"description"))
    {
      console.log("abilityMaladumViewer, compétence avec objet description ")
      textTooltip = textTooltip+ " " + filteredAbility[0].abilityDetail.description
    }
    else
    {
      console.log("abilityMaladumViewer, compétence SANS objet description - on affiche rien dans le tootip ")
    }
  }

}

// gestion de l'alignement du toolti^p, à gauche ou à droite.
var l_class = "tooltiptext"
if (props.tooltipOnLeft) {
  l_class = l_class + " tooltiplefttext"

}
else {
  l_class = l_class + " tooltiprighttext"
}

</script>

<template>
  <span :class="l_class" v-html="textTooltip"></span>
</template>

<style>

/* Tooltip text */
.tooltip .tooltiplefttext {
  top: -5px;
  right: 105%;
}

.tooltip .tooltiprighttext {
  top: -5px;
  left: 105%;
}
</style>
