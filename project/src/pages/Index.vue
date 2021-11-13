<template>
  <div id="scroll" style="height: 100%">
    <Introduction s="0" />
    <CurrentSituation s="1" />
    <SDG s="2"/>
    <RegionalComparison s="3" />
    <MeetTargets s="4"/>
    <Actions s="5"/>
  </div>
</template>

<script>
import Introduction from 'components/Introduction';
import CurrentSituation from 'components/CurrentSituation';
import SDG from 'components/SDG'
import RegionalComparison from 'components/RegionalComparison';
import MeetTargets from "components/MeetTargets"
import Actions from "components/Actions";

export default {
  name: 'PageIndex',
  components: {
    Introduction,
    CurrentSituation,
    SDG,
    RegionalComparison,
    MeetTargets,
    Actions,
  },
  data() {
    return {};
  },
  methods: {},
  mounted() {
    let c = document.getElementById('scroll').children;
    const onScroll = () => {
      c.forEach((e, i) => {
        let p = e.getBoundingClientRect();
        if (p.y >= -p.height - 150 && p.y <= 150) {
          this.$store.commit('sider/updateIndex', i);
        }
      });
    };
    window.document.addEventListener('scroll', onScroll);
  },
};
</script>
