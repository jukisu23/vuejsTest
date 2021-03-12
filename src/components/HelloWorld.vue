<template>
  <div class="super">
    <div class="container real">
      <section v-for="section of data" :key="section.id" :id="'parent' + section.id">
        <div class="card mainItem">
          <h2>{{ section.title }}</h2>
          <p class="mainText">{{ section.text }}</p>
        </div>
        <div
          class="card childItem"
          v-for="child in section.childs"
          :key="child.title"
          :id="'child'+child.id"
        >
          <h2>{{ child.title }}</h2>
          <p class="mainText">{{ child.text }}</p>
        </div>
      </section>
    </div>

    <div class="container invis">
      <section v-for="section of data" :key="section.title">
        <div class="card mainItem">
          <h2>{{ section.title }}</h2>
          <p class="mainText">{{ section.text }}</p>
        </div>
        <div
          class="card childItem"
          v-for="child in section.childs"
          :key="child.title"
        >
          <h2>{{ child.title }}</h2>
          <p class="mainText">{{ child.text }}</p>
        </div>
      </section>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import CheckboxComponent from "./Checkbox.vue";
import VueScrollTo from "vue-scrollto";

Vue.use(VueScrollTo);

const options = {
  container: ".container.real",
  easing: "ease-in",
  offset: -60,
  force: true,
  cancelable: true,
  onStart: function(element) {
    // scrolling started
  },
  onDone: function(element) {
    // scrolling is done
  },
  onCancel: function() {
    // scrolling has been interrupted
  },
  x: false,
  y: true
};

@Component({
  components: {
    CheckboxComponent
  }
})
export default class HelloWorld extends Vue {
  private data: Array<any> = [
    {
      id: 0,
      title: "foo",
      text: "lorem ipsum",
      childs: [
        {
          id: 1,
          title: "bar",
          text: "lorem ipsum"
        },
        {
          id: 2,
          title: "baz",
          text: "lorem ipsum"
        }
      ]
    },
    {
      id: 1,
      title: "foo",
      text: "lorem ipsum",
      childs: [
        {
          id: 3,
          title: "bar",
          text: "lorem ipsum"
        },
        {
          id: 4,
          title: "baz",
          text: "lorem ipsum"
        }
      ]
    }
  ];

  private currentchild = 0;
  private lastscroll = 0;

  private scrollHandler(e) {
    console.log("scroll", this.lastscroll, window.scrollY, e);
    if (window.scrollY - this.lastscroll > 200) {
      console.log("PENG");
      this.lastscroll = window.scrollY;
      document.getElementById("parent0").style.left = (-1*this.currentchild*window.innerWidth)+"px";
      this.currentchild++;
    }
  };

  constructor() {
    super();
    window.addEventListener("scroll", this.scrollHandler);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
html,
body {
  height: 100vh;
  padding: 0;
  margin: 0;
}
h2 {
  margin: 40px 0 0;
}
section {
  height: 100%;
}
.real section {
  display: -webkit-box;
}
vue-scroll {
  height: 100%;
}
.card {
  width: 100%;
  background-color: aqua;
  height: 100%;
  margin-bottom: 1em;
  border: 1px solid black;
}
.mainItem {
  background-color: greenyellow;
}
.container {
  height: 100%;
  width: 100%;
}
.childItem {
}

.invis {
  visibility: hidden;
}
.super {
  height: 100%;
}
.real {
  position: fixed;
}
</style>
