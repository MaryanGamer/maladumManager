<script setup>

import { ref } from 'vue'
// - un objet campagne (campaign), composé de :
//  - Nom de la campagne : campaignName
//  - Retard : campaignDelay
//  - Prochain scenario : campaignNextScenario
//  - autres infos (un blob de données : campaignOtherInfos) (un string, en fait)
const campaign = defineModel()

function updateDelay(u) {
  campaign.value.campaignDelay = parseInt(campaign.value.campaignDelay) + u
  if (campaign.value.campaignDelay < 0) {campaign.value.campaignDelay = 0}
  if (campaign.value.campaignDelay > 30) {campaign.value.campaignDelay = 30}

}

const toShowCampaignDetails = ref(false)
function showCampaignDetails() {
  toShowCampaignDetails.value = !toShowCampaignDetails.value
}

</script>

<template>
<div class="pure-g global-campaign">
  <div class="pure-u-1" id="detailCampaign"> <button @click="showCampaignDetails">{{ toShowCampaignDetails ? '-' : '+' }}</button> Votre Campagne
  </div>
  <div class="pure-u-1">
    <div v-if="toShowCampaignDetails" class="pure-g">
      <div class="pure-u-1 pure-u-sm-1-2 pure-u-lg-1-4">
        <br/><input v-model="campaign.campaignName" placeholder="nom de la Campagne" />
      </div>
      <div class="pure-u-1 pure-u-sm-1-2 pure-u-lg-1-4">
        Retard <br/> <button @click="updateDelay(-1)">-</button> {{ campaign.campaignDelay }} <button @click="updateDelay(+1)">+</button>
      </div>
      <div class="pure-u-1 pure-u-sm-1-2 pure-u-lg-1-4">
        Prochain scenario <br/> <input v-model="campaign.campaignNextScenario" placeholder="What's next ?" />
      </div>
      <div class="pure-u-1 pure-u-sm-1-2 pure-u-lg-1-4">
        Notes <br/> <textarea id="notes" v-model="campaign.campaignOtherInfos"> </textarea>
      </div>
    </div>
  </div>
</div>


</template>

<style>

</style>
