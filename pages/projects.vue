<template>
  <div class="_p_index">
    <div :class="$style.screens">
      <div :class="$style.pageFlex">
        <div :class="$style.page">
          <h2 :class="$style.h3">Where Ideas Come Alive ✨</h2>
          <br>
          <p :class="$style.block">Here, you'll find a curated selection of projects I've completed.<br>And there are some that I still always update because of the good cooperative relationship with clients</p>
          <br><br>
          <div :class="$style.projectGrid">
            <c-card
              v-for="(item, index) in projects"
              :key="index"
              :technologies="item.technologies"
              :screenshoot="require(`@/assets/img/projects/${item.screenshoot}`)"
              :category="item.category"
              :name="item.name"
              :description="item.description"
              :link="item.link"
            />
          </div>
          <div :class="$style.projectAction">
            <a href="javascript:void(0)" :class="$style.button" @click="viewProjectStatus()">
              <template v-if="!projectViewStatus">View more</template>
              <template v-else>View less</template>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "@/components/basics/card"
export default {
  head: {
    title: 'Project - Ramadhan',
  },
  components: {
    "c-card": Card
  },
  data() {
    return {
      projects: [],
      projectsStore: [],
      projectViewStatus: false
    };
  },
  mounted() {
    this.$ga.page({
      page: '/project',
      title: 'Project',
      location: window.location.href
    })
    this.getProject();
  },
  methods: {
    async getProject() {
      try {
        const projectStore = this.$store.state.projects;

        this.projects = projectStore.slice(0, 8);
        this.projectsStore = projectStore;
      } catch (err) {
        this.projects = [];
        console.error(err);
      }
    },
    viewProjectStatus() {
      if (this.projectViewStatus) {
        this.projectViewStatus = false;
        this.projects = this.projectsStore.slice(0, 8);
      } else {
        this.projectViewStatus = true;
        this.projects = this.projectsStore;
      }
    }
  }
}
</script>

<style module lang="sass" src="@/assets/sass/modules/pages.sass"></style>