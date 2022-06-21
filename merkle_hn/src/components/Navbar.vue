<!-- Template -->

<template>
    <header :class="{'scolled-nav': scrollPosition }">
        <nav>
            <div class="branding">
                <img src="@/assets/merkle_logo.png" alt="">
            </div>

            <ul v-show="!mobile" class="navigation">
                <li><router-link class="link" :to="{name: ''}">Home</router-link></li>
                <li><router-link class="link" :to="{name: ''}">About</router-link></li>
                <li><router-link class="link" :to="{name: ''}">Contact</router-link></li>
            </ul>
            <div class="icon">
                <i @click="toggleMobileNav" v-show="mobile" class="far fa-bars" :class="{'icon-active': mobileNav}"></i>
            </div>
            <transition name="mobile-nav">
                <ul v-show="mobileNav" class="dropdown-nav">
                    <li><router-link class="link" :to="{name: ''}">Home</router-link></li>
                    <li><router-link class="link" :to="{name: ''}">About</router-link></li>
                    <li><router-link class="link" :to="{name: ''}">Contact</router-link></li>
                </ul>
            </transition>
        </nav>
    </header>
</template>


<!-- Script -->
<script>
export default {
    name: 'NavMenu',
    data() {
        return {
            scrollPosition: null,
            mobile: true,
            mobileNav: null,
            windowWidth: null,
        };
    },
};
</script>


<!-- Style -->
<style lang="scss" scoped>
    header {
        background-color: rgba(0, 0, 0, 0.8);
        z-index: 99;
        width: 100%;
        position: fixed;
        transition: .5s ease all;
        color: white;

        nav{
            display: flex;
            flex-direction: row;
            padding: 12px 0px;
            transition: .5s ease all;
            width: 90%;
            margin: 0 auto;

            @media(min-width: 1140px) {
                max-width: 1140px;
            }

            ul,
            .link{
                font-weight: 500;
                color: #fff;
                list-style: none;
                text-decoration: none;

            }

            li {
                text-transform: uppercase;
                padding: 16px;
                margin-left: 16px;
            }

            .link {
                font-size: 14px;
                transition: .5s ease all;
                padding-bottom: 4px;
                border-bottom: 1px solid transparent;

                &:hover {
                    color:#00afea;
                    border-color: #00afea;
                }
            }

            .branding {
                display: flex;
                align-items: center;
                img {
                    width:50px;
                    transition: .5s ease all;
                }
            }
        }
    }

</style>