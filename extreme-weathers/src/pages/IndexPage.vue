<template>
  <div id="scroll" style="height: 100%">
    <CoverPage />
    <IntroSession />
    <SessionBanner
      img-url="images/banner1.jpg"
      title="Global Situation"
      subtitle=""
    />
    <GlobalSituation />
    <SessionBanner
      img-url="images/banner2.jpg"
      title="Heatwaves in Europe"
      subtitle=""
    />
    <EuropeanSituation />
    <SessionBanner img-url="images/banner3.jpg" title="Outlook " subtitle="" />
    <OutlookSession />
    <SourceSession />
  </div>
</template>

<script>
import { defineComponent } from "vue";
import CoverPage from "components/utils/CoverPage";
import IntroSession from "components/contents/IntroductionSession";
import SessionBanner from "components/utils/SessionBanner.vue";
import GlobalSituation from "components/contents/GlobalSituation.vue";
import EuropeanSituation from "src/components/contents/EuropeanSituation.vue";
import OutlookSession from "src/components/contents/OutlookSession.vue";
import SourceSession from "src/components/utils/SourceSession.vue";

export default defineComponent({
  name: "IndexPage",
  components: {
    IntroSession,
    CoverPage,
    SessionBanner,
    GlobalSituation,
    EuropeanSituation,
    OutlookSession,
    SourceSession,
  },
});
</script>
