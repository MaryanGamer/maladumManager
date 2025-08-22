<script setup>

  //import { ref, computed,onMounted } from 'vue'
  import headerMaladum from './headerMaladum.vue'
  import gameMaladum from './gameMaladum.vue'

</script>

<template>

  <div class="pure-g global-back">
    <div class="pure-u-1-1">
      <headerMaladum />
    </div>
    <div class="pure-u-1-1">
      <gameMaladum />
    </div>
  </div>
  MDR - no copyright - V1.1

</template>

<style>

.pure-g > div {
        box-sizing: border-box;
    }

.global-back {
    background: rgb(223, 217, 20);
    padding:  5px;
}

.global-header {
    background: rgb(242, 241, 206);
    padding:  5px;
}

.global-game {
    background: rgb(153, 209, 142);
    padding:  5px ;

}

.global-campaign {
    background: rgb(76, 170, 199);
    padding:  5px;


}
.global-team {
    background: rgba(98, 207, 240, 0.877);
    padding:  5px;
}
.global-team-info {
    background: rgba(214, 233, 238, 0.877);
    padding:  5px;
}
.global-member {
    background: rgba(193, 210, 232, 0.877);
    padding:  5px;
}
.global-training {
    background: rgba(222, 227, 246, 0.877);
    padding:  5px;
}
.global-powers {
    background: rgba(222, 227, 246, 0.877);
    padding:  5px;
}
.global-recruit {
    background: rgba(210, 200, 241, 0.877);

}

.alignGlobal{
  display: flex;
  justify-content: center;
  align-items: center;

}


.title {
  color: rgb(149, 147, 218);
}

.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black; /* If you want dots under the hoverable text */
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  /**min-width : 120px ;
  max-width : 360px ; */
  width : 300px ;
  background-color: black;
  color: #fff;
  /**text-align: center;*/
  padding: 5px 0;
  border-radius: 6px;

  /* Position the tooltip text - see examples below! */
  position: absolute;
  z-index: 1;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
  visibility: visible;
}

</style>
