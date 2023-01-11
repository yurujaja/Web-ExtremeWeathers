<template>
  <LimitWidth
    ><div>
      <h4><p>What Are Extreme Events?</p></h4>
      <div class="text-body1">
        <p>
          Extreme weather refers to unusual or severe weather events that are
          outside the range of normal weather patterns. These events can include
          extreme heat, cold, storms, floods, droughts, and other natural
          disasters.
        </p>
        <q-space></q-space>
        <p>
          In recent years, the earth has witnessed extreme events going from bad
          to worse, breaking records with alarming frequency. Heatwaves in
          Europe. Colossal floods in Pakistan. Prolonged and severe droughts in
          China, the Horn of Africa and the United States. There is nothing
          natural about the new scale of these disasters.
        </p>
        <q-space></q-space>
        <p>
          It is important to understand and prepare for extreme weather events
          in order to minimize their impacts. Especially, understanding the
          risks associated with different types of extreme weather events can
          help people prepare for and respond to them effectively.
        </p>
      </div>
      <h4><p>Types of Weather Extremes</p></h4>
      <div class="text-body1">
        <p>
          Definitions of extreme weather vary in different parts of the
          scientific community, changing the outcomes of research from those
          fields. Below introduces four main types of extreme weathers that
          occur quite often and are significantly related to the human-being.
        </p>
      </div>
    </div></LimitWidth
  >

  <div>
    <TypesCard />
  </div>
</template>

<script>
import { ref } from "vue";
import TypesCard from "./ExtremesTypes.vue";
import LimitWidth from "../utils/LimitWidth.vue";

export default {
  name: "IntroSession",
  components: {
    TypesCard,
    LimitWidth,
  },
  setup() {
    return {
      slide: ref("first"),
      autoplay: ref(true),
    };
  },
};
</script>

<style lang="sass" scoped>
strong
  color: #ff6600
  font-size: 105%


.text-body1
  text-align: left
  font-size: 150%



.custom-caption
  text-align: center
  padding: 12px
  color: white
  background-color: rgba(0, 0, 0, .3)
</style>
