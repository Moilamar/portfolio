<template>
    <b-navbar
        sticky
        type="light"
        id="navbar"
        :class="{ 'show-banner': loaded }"
    >
        <div id="nav-container">
        <b-navbar-brand
            id="brand"
            href="#banner"
            v-scroll-to="'#banner'"
            :class="{ 'show': showBrand }"
        >
            <img src="../assets/logo.png" alt=""/>
            <div>
                <span id="markus">Markus </span>
                <span id="moilanen">Moilanen</span>
            </div>
        </b-navbar-brand>

        <div
            id="nav-collapse-btn"
            v-b-toggle.collapse
        >
            <i class="fa fa-bars" />
        </div>

        <b-navbar-nav id="nav-list">
            <b-nav-item v-scroll-to="'#about'">About</b-nav-item>
            <b-nav-item v-scroll-to="'#projects'">Projects</b-nav-item>
            <b-nav-item v-scroll-to="'#skills'">Skills</b-nav-item>
            <b-nav-item v-scroll-to="'#contact'">Contact</b-nav-item>
        </b-navbar-nav>

        <b-collapse id="collapse">
            <div id="collapse-nav-list">
                <div v-scroll-to="'#about'" v-b-toggle.collapse>About</div>
                <div v-scroll-to="'#projects'" v-b-toggle.collapse>Projects</div>
                <div v-scroll-to="'#skills'" v-b-toggle.collapse>Skills</div>
                <div v-scroll-to="'#contact'" v-b-toggle.collapse>Contact</div>
            </div>
        </b-collapse>
        </div>
    </b-navbar>
</template>

<script>
export default {
    data() {
        return {
            loaded: false,
            showBrand: false
        };
    },
    mounted() {
        setTimeout(() => {
            this.loaded = true;
        }, 100);
        let waypoint = new Waypoint({
            element: document.getElementById("navbar"),
            handler: () => {
                this.showBrand = true;
                waypoint.destroy();
            }
        });
    },
    props: ["scrolled"]
};
</script>

<style lang="scss">
@import "../styles/variables.scss";
@import "../styles/mixins.scss";

#navbar {
    @include transition(margin-top, 1.5s, ease);
    @include flexbox(column, center);
    height: 7vh;
    @media screen and (max-width: $sizeSm) {
        height: 9vh;
    }
    background-color: rgba(255, 255, 255, 0.95);
    z-index: 999;
    @include box-shadow(
        0 2px 4px 0 rgba(40, 40, 40, 0.2),
        0 3px 10px 0 rgba(40, 40, 40, 0.2)
    );
    top: -1px;
    #nav-container {
        @include flexbox(row, center);
    #brand {
        width: 0;
        opacity: 0;
        pointer-events: none;
        @include transition(all, 1.5s, ease);
        @include flexbox(row, center, center);
        img {
            width: auto;
            height: 4vh;
            @media screen and (max-width: $sizeSm) {
                height: 6vh;
            }
        }
        div {
            font-family: $fontBrand;
            font-size: 3.5vh;
            font-weight: bold;
            font-variant: small-caps;
            margin-left: 12px;
            @media screen and (max-width: $sizeMd) {
                font-size: 3.5vh;
            }
        }
        #moilanen {
            color: $colorSecondary;
        }
    }
    .show {
        width: auto !important;
        opacity: 1 !important;
        pointer-events: initial !important;

    }
    #nav-collapse-btn {
        font-size: 3.5vh;
        color: #444;
        opacity: 0;
        margin-left: 0.5em;
        @include flexbox(column, center);
        @media screen and (min-width: $sizeSm) {
            display: none;
        }
    }
    #nav-list {
        margin-left: 1em;
        -webkit-backface-visibility: hidden;
        @include flexbox(row, center, center);
        @media screen and (max-width: $sizeSm) {
            display: none;
        }
        .nav-item {
            cursor: pointer;
            height: 7vh;
            width: auto;
            padding: 0 1.5em 0 1.5em;
            @include flexbox(row, center, center);
            text-align: center;
            @include transition(background-color, 0.7s, ease);
            a {
                color: #555;
                font-size: 115%;
                font-weight: bold;
                font-family: $fontBrand;
                transition: color 0.5s;
                margin-top: 3px;
            }
        }
        .nav-item:hover {
            background-color: $colorSecondary;
            a {
                color: white;
            }
        }
    }
    #collapse {
        position: fixed;
        right: 0;
        top: 8.7vh;
        #collapse-nav-list {
            @include flexbox(column);
            background: $colorLighter;
            div {
                @include flexbox(column, center, center);
                height: 35px;
                font-size: 105%;
                padding: 0 20px 0 20px;
            }
        }
    }
    }
}
.show-banner {
    margin-top: 0 !important;
}
</style>
