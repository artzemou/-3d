<template>
  <div id="app">
    <header>
      <!--<div class="logo">
        <img alt="" src="./assets/@@logo.svg"/>
        <span>Donnez forme à vos projets.</span>
      </div>-->
      <div class="logo">
        <img alt src="./assets/logo-@m-it.svg.png" />
        <span></span>
      </div>
      <!--<a id="save" download href="./assets/@logo.svg">enregistrer</a>-->
    </header>
    <ul id="panels" v-for="(panel, index) in panels" :key="index">
      <li>
        <i :style="{  backgroundImage: `url('${panel.icon}')`}"></i>
        <span
          @click="onPanelClick(index, $event)"
          :class="[current === index ? `current ${panel.className}` : panel.className]"
        >{{panel.title}}</span>
      </li>
      <li
        :class="[isOpen.includes(index) ? 'description open' : 'description']"
      >{{panel.description}}</li>
    </ul>
    <!-- <section class="container">
      <div id="box" :class="`box ${panels[current].className}`">
        <figure class="front"></figure>
        <figure class="back"></figure>
        <figure class="right"></figure>
        <figure class="left"></figure>
        <figure class="top"></figure>
        <figure class="bottom"></figure>
      </div>
    </section>-->
    <p class="link"></p>
  </div>
</template>
<script>
/* eslint-disable */
import HelloWorld from "@/components/HelloWorld";

export default {
  name: "App",
  components: { HelloWorld },
  mounted() {},
  data: function() {
    return {
      animation: null,
      panels: [
        {
          className: "show-front",
          title: "@m-it ?",
          icon: require("@/assets/slapch.svg"),
          description:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum, esse illo aperiam eligendi asperiores magni consequatur nulla commodi provident, ipsa nobis magnam beatae possimus sequi delectus "
        },
        {
          className: "show-back",
          title: "Notre réseau",
          icon: require("@/assets/slapch.svg"),
          description:
            "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Repellendus facere ipsam necessitatibus? Accusantium soluta, corporis corrupti quod aliquam natus ex laborum fuga, veniam cum rerum facilis?  provident vitae?"
        },
        {
          className: "show-right",
          title: "Contact",
          icon: require("@/assets/slapch.svg")
        }
      ],
      isOpen: []
    };
  },
  computed: {
    current() {
      return this.$store.state.current;
    }
  },
  methods: {
    onPanelClick: function(i, e) {
      this.isOpen.includes(i)
        ? this.isOpen.splice(this.isOpen.indexOf(i), 1)
        : this.isOpen.push(i);
      clearInterval(this.animation);
      this.$store.commit("setCurrent", i);
    },
    beforeEnter: function(el) {
      el.style.opacity = 0;
      el.style.height = 0;
    },
    enter: function(el, done) {
      var delay = el.dataset.index * 150;
      setTimeout(function() {
        Velocity(el, { opacity: 1, height: "1.6em" }, { complete: done });
      }, delay);
    }
  }
};
</script>

<style lang="scss">
@import "normalize.css";
@import "compass/css3";
@import url("https://fonts.googleapis.com/css?family=Lato:100,100i,300,300i,400,400i,700,700i,900,900i");
$box-width: 60px;
$box-height: $box-width;
$primary-color: #ffffff;
$secundary-color: #0061d7;
$secundary-color: #ffffff;

* {
  margin: 0;
  padding: 0;
  @include box-sizing(border-box);
}
body {
  text-align: center;
  background: url(../static/assets/path1065-4-0-1-3-5-0-61.png) 80% 80% / 30%
    no-repeat;
  font-family: Lato;
  color: #333333;
  @include perspective(1200px);
  height: 100vh;
}
h1 {
  font-weight: normal;
  font-size: 40px;
  font-weight: normal;
  margin: 20px 0 10px 10px;
  span {
    display: block;
    padding-left: 4px;
  }
}
img {
  max-width: 75px;
}
header {
  background: #f9f9f9;
  box-shadow: 0 0 2px #d9d9d9;
  padding: 2rem 0;
  margin-bottom: 2rem;
  .logo {
    display: flex;
    height: 120px;
    margin: 0 3rem;
    img {
      max-width: 150px;
    }
    span {
      margin: 80px 10px;
      font-weight: bold;
    }
  }
}

.container {
  width: $box-width;
  height: $box-height;
  position: relative;
  margin: 40px auto;
  //border: 1px solid #CCC;
  @include perspective(1200px);
}

.box {
  width: 100%;
  height: 100%;
  position: absolute;
  @include transform-style(preserve-3d);
  @include transition(transform 0.5s);

  figure {
    display: table;
    position: absolute;
    text-align: center;
    color: white;
  }
}

//Sizes
.box .front,
.box .back {
  width: $box-width;
  height: $box-height;
}
.box .right,
.box .left {
  width: $box-width;
  height: $box-height;
}
.box .top,
.box .bottom {
  width: $box-width;
  height: $box-width;
}

//Positions
.box .right,
.box .left {
  left: $box-width;
}
.box .top,
.box .bottom {
  top: $box-height;
}

//Colors
// .box .front,
.box .back {
  background: url(../static/assets/logo-@m-it.svg.png);
  background-size: 100%;
  background-repeat: no-repeat;
}
.box .right,
.box .left,
.box .top,
.box .bottom {
  // background: darken($secundary-color, 0%) url(../static/assets/motif.svg);
  background-size: 300%;
  background-repeat: no-repeat;
}

//Transforms
.box .front {
  @include transform(translateZ($box-height / 2));
}
.box .back {
  @include transform(rotateX(-180deg) translateZ($box-height / 2));
}
.box .right {
  @include transform(rotateY(90deg) translateZ($box-width / -2));
}
.box .left {
  @include transform(rotateY(-90deg) translateZ($box-width * 1.5));
}
.box .top {
  @include transform(rotateX(90deg) translateZ($box-height / 2));
}
.box .bottom {
  @include transform(rotateX(-90deg) translateZ(-$box-height * 1.5));
}

//Show Specific Face
.box.show-front {
  @include transform(
    translateZ($box-height / -4) rotateZ(3deg) rotateY(-30deg)
  );
}
.box.show-back {
  @include transform(
    translateZ($box-height / -4) rotateX(-180deg) rotateZ(-8deg) rotateY(-12deg)
  );
}
.box.show-right {
  @include transform(
    translateZ($box-width / -2) rotateY(-90deg) rotateZ(12deg) rotateY(12deg)
  );
}
.box.show-left {
  @include transform(
    translateZ($box-width / -2) rotateY(90deg) rotateZ(12deg) rotateY(-12deg)
  );
}
.box.show-top {
  @include transform(
    translateZ($box-height / -2) rotateX(-90deg) rotateZ(120deg) rotateY(54deg)
  );
}
.box.show-bottom {
  @include transform(
    translateZ($box-height / -2) rotateX(90deg) rotateZ(12deg) rotateY(-120deg)
  );
}

//Rollover
.box:hover {
  //@include transform(rotateX(-180deg) translateZ($box-height / 4));
}

//Buttons
ul#panels {
  list-style: none;
  padding-left: 5rem;
  .description {
    padding: 0;
    padding-left: 50px;
    max-height: 0;
    overflow: hidden;
    text-align: left;
    font-size: 12px;
    max-width: 300px;
    font-weight: 300;
    @include transition(all 0.3s linear);

    &.open {
      max-height: 13vh;
      padding: 10px;
      padding-left: 50px;
    }
  }
  li {
    display: flex;
    text-align: left;
    padding: 10px;
    &:hover {
      //background: darken($secundary-color, 15%);
      i {
        @include transform(rotate(13deg));
      }
    }
    i {
      background-size: 100%;
      background-repeat: no-repeat;
      background-position: 3% 50%;
      margin-right: 5px;
      min-width: 30px;
      height: 30px;
      @include transition(all 0.2s ease-in);
    }
    span {
      flex: 1;
      outline: none;
      cursor: pointer;
      border: none;
      color: #444444;
      font-family: "Lato";
      font-size: 14px;
      font-weight: bold;
      white-space: nowrap;
      margin: auto;
      padding-left: 5px;
      //background: darken($secundary-color, 5%);
      @include border-radius(2px);
      @include transition(all 0.2s ease-in);
      &:hover {
        //background: darken($secundary-color, 15%);
        i {
          @include transform(rotateX(1800deg));
        }
      }
      &.current {
        //background: darken($secundary-color, 20%);
      }
    }
  }
}

p.link {
  clear: both;
  margin-top: 40px;
  a {
    text-transform: uppercase;
    text-decoration: none;
    display: inline-block;
    color: #fff;
    padding: 5px 10px;
    margin: 0 5px;
    background-color: darken($secundary-color, 5);
    @include transition(all 0.2s ease-in);
    &:hover {
      background-color: darken($secundary-color, 20);
    }
  }
}
</style>
