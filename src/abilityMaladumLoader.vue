<script setup>
import { ref,onMounted } from 'vue'
//permet de gérér des règles et abilité

// abilityKey , c'est :
//  un nom
//  optionel : un nom anglais nomEN
//  un type (Magie/Sort/Compétence/Pouvoir/Regle)

// un abilityDetail , c'est la decription d'une abilité.
//  une description
//  Une 'category' si type Compétence (famille de compétence) ou sort (ecole)
//  seuil , si type = sort ou Compétence ou Magie, ca peut être le max ateignable, ou le niveau de sort
//  un tableau 'descriptionNiveaux', si type compétence, avec en taille le seuil
//    dans le tableau, chaque entrée est la description
//  un logo, une URL d'image qui pourra servir à l'avenir.

// abilities est un tableau de référence avec toutes la abilités existant dans le jeu
// chaque élément est consitué
//  d'un abilityKey
//  d'un abilityDetail

// le tableau 'aptitudes' est une liste des abilités disponibles, pour la formation du personnage.
// chaque élément est une abilityCursus : une abilité disponible dans un cursus de carrière ou un cursus de personnage, jusqu'à un certain niveau
// un abilityCursus, c'est
  //  un abilityKey
  //  un niveau max accessible : cursusMaxLevel
    // si type de l'abilité = Compétence : cela donne le seuil maximal atteignable (même si l'abilité peut aller plus haut, encore)
    // si type = Magie : C'est le nombre de sorts apprenables
    // si type = sort : ne sert à rien
    // si type = Pouvoir, cela donne le niveau de pouvoir accordé
  // en cas de compétence on peut avoir un niveau initial, pour les compétences issues du personnage : cursusInitialLevel
    // lorsque cette donnée est renseignée, cela signifie implicitement que cette compétence vient du personnage, et non de la classe.
  // si cette abilité dans le cursus occupe un espace d'armure, dans le cas du cursus de companion, alors il y a un champ cursusSlotArmor à true
// 'aptitudes' peut être dans une classe, ou un companion

//  member.value.memberInfos.xpUsage.push ({id:l_XPUsageMaxID, xpUsed : true, acquiredAbility :l_abilityAcquired})

// une acquiredAbility est un niveau d'abilité acquis grace à un ou plusieurs point d'expérience.
// On peut retrouver cela pour représenter
  // dans le tableau XPUsage, à quoi a servi chaque XP, en terme d'amélioration.
  // l'ensemble des formations du personnage : tableau allAcquiredAbilities
// c'est
//  un id
//  un abilityKey
//  un 'acquiredLevel', utile pour pouvoir (fixée à la creation), Compétence (niveau acquis) ou magie (fixé à la creation)
    // dans XPUsage , indique le niveau d'acquisition avec cet XP
    // allAcquiredAbilities : le niveau max acquis.

// un allAcquiredAbilities est un ensemble d'abilités acquises

const Abilities = ref([

{    "abilityKey" :  { "nom":"Reflexes","type":"Compétence"  },
         "abilityDetail" : { "category" : "Agilité" , "seuil":"3",
			descriptionNiveaux :
			[
				"1:reaction; quand un ennemi engage le personnage, celui ci se déplace sans AdO. Passif, Ignorez une touche sur les AdO.","2:reaction; quand un ennemi engage le personnage, Dans l'ordre de votre choix, celui ci se déplace sans AdO et attaque. Passif, le personnage peut utiliser Parade contre les tirs.","3:reaction; quand un ennemi engage le personnage, l'attaquant est étourdi et le personnage effectue 2 déplacement, sans AdO, et 1 attaque (ordre à votre choix). Passif, pour un action rapide, vous pouvez ignorer une AdO."
			]
		}
} ,


{    "abilityKey" :  { "nom":"Camouflage","type":"Compétence"  },
         "abilityDetail" : { "category" : "Voleur" , "seuil":"3",
			descriptionNiveaux :
			[
			"Tant que vous êtes en contact avec un mur, pour ne pouvez pas être cible jusque la fin du round. Les enemis traversent vos cases adjacentes sans s'arréter ni déclencher d'AdO. Mais ils ne peuvent pas s'arréter dans une case qui vous est adjacent. Vou sne bloquez pas les LdV.",
			"2 : effectuez un tir ou un déplacement. Puis, appliquez le niveau 1 si vous êtes en contact avec un décor.",
			"3:Comme le niveau 1 tant que vous n'êtes pas en contact avec un ennemi. réation Passive : à utiliser n'importe quandpendant un round ou Camouflage est actif; vous effectuez un tir et prenez un jeton fatigue."
			]
		}
} ,
{    "abilityKey" :  { "nom":"Plonger à couvert","type":"Compétence"  },
         "abilityDetail" : { "category" : "Voleur" , "seuil":"3",
			descriptionNiveaux :
			[
				"1:Réaction : A utiliser lorsque vous êtes la cible d'un tior ou d'un sort et qu'il est à moins de 4 cases d'un couvert. Il se déplace vers ce couvert.",
				"2:Réaction : A utiliser lorsque vous êtes la cible d'un tior ou d'un sort et qu'il est à moins de 4 cases d'un couvert. Il se déplace vers ce couvert (sans AdO).",
				"3:Réaction : N'importe quand, Dans l'ordre de votre choix, le personnage se déplace vers un couvert (sans AdO) et attaque.Il ne peut être ciblé jusqu'à la fin du rundtant qu'il reste dans sa position."
			]
		}
} ,

{    "abilityKey" :  { "nom":"Diversion","type":"Compétence"  },
         "abilityDetail" : { "category" : "Ruse" , "seuil":"3",
			descriptionNiveaux :
			[
				"1:un personnage en LdV et portée moyenne est fatigué",
				"2:effectuer un tior  ou lancez un objet. la cible ou un autre ennemi à portée courte de la cible gagne 2 marqueurs fatigue. Puis déplacez vous.",
				"3:Déplacez un personnage à portée moyenne en LdV; ce déplacement ne peut pas le forcer à se causer du tord, ni engager un ennemi.Il gagne 2 marqueurs fatigue. Avant ou après avoir provoqué cet effet, vous pouvez vous déplacer ou attaquer, dans ;'ordre de votre choix."
			]
		}
} ,
{    "abilityKey" :  { "nom":"Doigts Agiles","type":"Compétence"  },
         "abilityDetail" : { "category" : "Ruse" , "seuil":"3",
			descriptionNiveaux :
			[
				"1 : Réaction, Après avoir subi une attaque de mélée, sans déghâts. Prenez un objet dans l'inventairede l'attaquant, autre que celui utilisé pour attaquer.","2:Déplacez vous au contactd'un personnageUtiliser l'aéction PickPocket; Puis effectuez un déplacement sasn AdO.","3:Passif, Pickpocket est une action standard"
			]
		}
} ,
{    "abilityKey" :  { "nom":"Entourloupe","type":"Compétence"  },
         "abilityDetail" : { "category" : "Ruse" , "seuil":"3",
			descriptionNiveaux :
			[
				"1:Gagnez 2 touchez sur un test de persuasion","2:Persuasion sur un aventurier. si réussite, l'aventurier a un marqueur fatigue par tcouhe. Passif : +1 aux tests de persuasion.","3:Persuasion sur un aventurier avec +3 touches. toute sles options sont disponibles."
			]
		}
} ,

{    "abilityKey" :  { "nom":"Pistage","type":"Compétence"  },
         "abilityDetail" : { "category" : "Survie" , "seuil":"3",
			descriptionNiveaux :
			[
				"1:consulter les 3 premières cartes evènement.","2:Effectuez tous les lancer d'entrée en jeu des PNJ, pour ce round. (Les points d'entrée en jeu à portée courte de l'aventurier ne peuvent pas être utilisés. Vous pouvez replacer tous les PNJ d'un point d'entrée vers un autre. Passif;Si votre point d'entrée est changé, lancer le dé magique 2 fois, ,et choisissez parmi les 2 résultats.","3:Reaction - avant ou après qu'un ennemi entre en LdV ou se place qsur une zone d'entrée, en interrompatn son déplacement.  le personnage fait un tour gratuit.tous ses alliées à portée courte peuvent faire une action (toute action envers l'ennemi arrivant gagne +1 dé). Passif - Le personnage réduit de 2 les valeurs de terrain difficile."
			]
		}
} ,

{    "abilityKey" :  { "nom":"Artiste","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "citoyen" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "Retirez un marqueur Fatigue d'un autre personnage à courte portée.; Phase de repos : ajoutez jusqu'à 2 à n'importe quel jet d'auberge sans dépenser de renommée",
              "À utiliser pendant le repos. Bénissez chaque personnage allié (y compris celui­ci) à courte portée. Vous pouvez augmenter le niveau de Terreur jusqu à deux pour bénir chaque personnage autant de fois supplémentaires. Phase de repos : à la fin de la phase, bénissez tous les personnages de votre groupe",
              "Ce personnage inspire tout son entourage à puiser dans sa force intérieure pour accomplir de grandes prouesses. Placez trois marqueurs Rappel sur le plateau de ce personnage. Tant qu'ils sont en place, tous les personnages alliés à courte portée peuvent utiliser leurs pions Magie comme s'il s'agissait de pions Compétence. Retirez un marqueur Rappel à chaque phase d'évaluation"
            ]
          }
  },

  {    "abilityKey" :  { "nom":"Don tactique","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "citoyen" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "Réaction : Travail d'équipe ! Lorsque ce personnage ou un autre personnage allié à courte portée et en LdV effectue une attaque, pour chaque personnage allié en contact avec lui ­même ou la cible de l'attaque, il peut soit ajouter un dé au jet, soit ajouter un maximum de X dés et gagner vicieux",
              "Réaction : une carte évennement est piochée, et fait apparaitre des personnages. Dans ce cas, le personnage portzeur de cette compétence et tous ceux à portée courte peuvent faire une action . Ils peuvent devenir fatigués et faire une seconde action. Passif : peut devenir fatigué pour faire une action durant le tour d'un alli; les 2 doivent être à portée courte.",
              "Dans une pièce sans ennemi, fermer toutes les portes, retorunéer tous les jetopn d'entrée à courte portée d'un personnage. tous les personnages de le pièce peuvent se repositionner. Pour chaque allié dans la pièce, remplacer un jeton noir par un jeton vert."
            ]
          }
  },

  {    "abilityKey" :  { "nom":"Récupération rapide","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "Endurance" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "le personnage regagne une épingle de santé",
              "à utiliser avant l'activation du personnagepour lui retirer le marqueur étourdiossement.Empoisonnement ou Multilation.",
              "Reaction - Quand le personnage est vaincu. le personnage regagne une épingle de santéet se remet sur pied. Passif - au début du tour du personnage, retirer un marqueur fatigue."
            ]
          }
  },
  {    "abilityKey" :  { "nom":"Promptitude","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "Agilité" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "faites un déplacement",
              "passif - gagne un point de mouvement.",
              "faites un déplacement; tous les déplacements du personnage sur ce tour ignorent les AdO. Effectuez une attaque avec 1 dé contre chaque ennemi avec lequel il entre en contact. Chaque touche (même sans dégats) met la cible au sol."
            ]
          }
  },
  {    "abilityKey" :  { "nom":"Intouchable","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "Voleur" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "A couvert, le personnage ne peut pas être la cible d'un tir jusque fin de tour.",
              "si A couvert ou au delà de portée courte, le personnage ne peut être une cible aux tirs.",
              "le personnage se déplace dans AdO. pas de tir ennemis sur lui possible ce tour."
            ]
          }
  },
  {    "abilityKey" :  { "nom":"Herboristerie","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "Citoyen" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "Reaction - Quand iune attaque alliée est effectuée à portée courte, elle gagne poison. si elle l'a déjà, elle gagne ///. Passif - utiliser les jetons herbes, champignons et minéraux en tant qu'action.",
              "Dépensez 2 actions pour fabriquer une potionavec un nombre illimités de H, F et Mplus un nombre d'autres ressources < au nombre de talents dépensés. Phase de commerce - Fabriquez un potion de la même manière.",
              "Piochez au hasard 3 jetons potions fabriquées et gardez en un. Après consommation, lancer un dé de combat pour chaque touche, l'utilisateur gagne une épingle. sur un echec, il est empoisonné."
            ]
          }
  },
  {    "abilityKey" :  { "nom":"formation","type":"Compétence"  },
          "abilityDetail" : {
            "category" : "Soutien" , "description" : "à fournir" , "seuil":"3" ,
            "descriptionNiveaux" :   [
              "Après une de vos action, une autre aventurier en portée courte et LdV effectue la même gratuitement.",
              "Phase de progression - un autre aventurier(rang max = talent dépensé) de votre équipe gagne 1 XP, assignable à une compétence d'agilité, d'endurance, de mélée, de tir ou de discrétion",
              "Phase de progression - 2 autres aventuriers gagnent un XP."
            ]
          }
  },

{"abilityKey" :  { "nom":"Amélioration de Malacyte","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "à fournir"   }  } ,

{"abilityKey" :  { "nom":"Immunité (Handicap)","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "ignore la condition Handicapant"   }  } ,
{"abilityKey" :  { "nom":"XP supplémentaires","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "gagne gratuitement 3 XPs à la création de personnage" }  } ,







{    "abilityKey" :  { "nom":"Détecter","type":"Sort"  },
          "abilityDetail" : {
            "category" : "Elémentaire",
            "description" : "À utiliser lors d'une action de recherche générale pour récupérer X objets supplémentaires (max. 3). dans la bourse. Les pièges sont résolus immédiatement. Tous les autres objets supplémentaires sont dispersés par le lanceur de sorts" ,
            "seuil" : "1" }  } ,
{    "abilityKey" :  { "nom":"Recupération","type":"Sort"  },
          "abilityDetail" : {
            "category" : "Proximité" ,
            "description" : "Action rapide : Retirer un jeton de fatigue; Action : Retirer un jeton empoisonné." ,
            "seuil" : "1" }  } ,





{    "abilityKey" :  { "nom":"Attaque mains nues","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "à fournir"   }  } ,
{    "abilityKey" :  { "nom":"Bénédiction","type":"Sort"  },
          "abilityDetail" : { "category" : "Vicarious"   }  } ,
{    "abilityKey" :  { "nom":"Bouclier de Malacyte","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité"   }  } ,
{    "abilityKey" :  { "nom":"Calme","type":"Sort"  },
          "abilityDetail" : { "category" : "Vicarious"   }  } ,
{    "abilityKey" :  { "nom":"Cocoon","type":"Sort"  },
          "abilityDetail" : { "category" : "Delta", "description" : "à fournir" ,"seuil":"3"   }  } ,


{    "abilityKey" :  { "nom":"Focus","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité", "seuil" : "1"   }  } ,
{    "abilityKey" :  { "nom":"Force","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité", "seuil" : "1"   }  } ,
{    "abilityKey" :  { "nom":"Fortitude","type":"Sort"  },
          "abilityDetail" : { "category" : "Vicarious"   }  } ,
{    "abilityKey" :  { "nom":"Frénésie","type":"Compétence"  },
          "abilityDetail" : { "category" : "Combat"   }  } ,
{    "abilityKey" :  { "nom":"Imperméable","type":"Compétence"  },
          "abilityDetail" : { "category" : "Endurance"   }  } ,
{    "abilityKey" :  { "nom":"Implacable","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "à fournir"   }  } ,
{    "abilityKey" :  { "nom":"Maitre d'armes","type":"Compétence"  },
          "abilityDetail" : { "category" : "Mélée"   }  } ,
{    "abilityKey" :  { "nom":"Manipulation de Pouvoir","type":"Compétence"  },
          "abilityDetail" : { "category" : "Magie"   }  } ,
{    "abilityKey" :  { "nom":"Manipulation de Pouvoir","type":"Compétence"  },
          "abilityDetail" : { "category" : "Magie"   }  } ,
{    "abilityKey" :  { "nom":"Manipulation de Pouvoir","type":"Compétence"  },
          "abilityDetail" : { "category" : "Magie"   }  } ,
{    "abilityKey" :  { "nom":"Peau de Fer","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité"   }  } ,
{    "abilityKey" :  { "nom":"Persuasion","type":"Compétence"  },
          "abilityDetail" : { "category" : "citoyen"   }  } ,
{    "abilityKey" :  { "nom":"Pistage","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Prêt à tout","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Protection","type":"Sort"  },
          "abilityDetail" : { "category" : "Vicarious"   }  } ,
{    "abilityKey" :  { "nom":"Reflexes","type":"Compétence"  },
          "abilityDetail" : { "category" : "Agilité"   }  } ,
{    "abilityKey" :  { "nom":"Remède Naturel","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Remède Naturel","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Remède Naturel","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Remède Naturel","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Renforcer","type":"Sort"  },
          "abilityDetail" : { "category" : "Procuration"   }  } ,
{    "abilityKey" :  { "nom":"Soin","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité"   }  } ,
{    "abilityKey" :  { "nom":"Troc","type":"Compétence"  },
          "abilityDetail" : { "category" : "Soutien"   }  } ,
{    "abilityKey" :  { "nom":"Uni avec la nature","type":"Compétence"  },
          "abilityDetail" : { "category" : "Survie"   }  } ,
{    "abilityKey" :  { "nom":"Vision nocturne","type":"Pouvoir"  },
          "abilityDetail" : { "description" : "à fournir"  }  } ,
{    "abilityKey" :  { "nom":"Vitesse","type":"Sort"  },
          "abilityDetail" : { "category" : "Proximité"   }  }
])

const emit = defineEmits(['listAllAbilities'])


async function fetchAbilitiesData() {
  //console.log("fetchAbilitiesData, avant chargement : liste des abilities en variable objet", Abilities.value)
  const res = await fetch(
    `./data/abilities.json`
  )
  //console.log("res : ",res)

  var l_text = await res.text()
  //console.log("text requete abilities : ",l_text)
  Abilities.value = await JSON.parse(l_text)
  console.log(Abilities.value)
  console.log ("abilityMaladumLoader, emit action")
  emit('listAllAbilities', Abilities.value)

}

fetchAbilitiesData()


onMounted(() => {}
)

//console.log ('referentiel des abilités : ',Abilities.value)

</script>
<template>
 <span/>
</template>

