<template>
  <div class="mobile-nav-group">
    <div
      class="mobile-nav-group__title mobile-nav-group__basetitle"
      :class="{
        'mobile-nav-group__title--open': isOpen
      }"
      @click="handleNavTitleClick">
      {{group.groupName}}
    </div>
    <div class="mobile-nav-group__list-wrapper" :class="{ 'mobile-nav-group__list-wrapper--open': isOpen }">
      <ul class="mobile-nav-group__list" :class="{ 'mobile-nav-group__list--open': isOpen }">
        <template v-for="navItem in group.list">
          <li
            class="mobile-nav-group__title"
            v-if="!navItem.disabled">
            <router-link
              active-class="active"
              :to="base + navItem.path">
              <p>
                {{ navItem.title }}
              </p>
            </router-link>
            <van-icon name="arrow"></van-icon>
          </li>
        </template>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    group: {
      type: Object,
      default: () => {
        return [];
      }
    },
    base: String,
    navKey: [String, Number]
  },

  data() {
    return {
      isOpen: false
    };
  },

  mounted() {
    this.isOpen = JSON.parse(sessionStorage.getItem('mobile-nav-' + this.navKey));
  },

  methods: {
    handleNavTitleClick() {
      this.isOpen = !this.isOpen;
      sessionStorage.setItem('mobile-nav-' + this.navKey, this.isOpen);
    }
  }
};
</script>

<style>
@component-namespace mobile {
  @b nav-group {
    border-radius: 2px;
    margin-bottom: 15px;
    background-color: #fff;
    box-shadow: 0 1px 1px 0 rgba(0,0,0,0.10);

    @e basetitle {
      padding-left: 20px;
    }

    @e title {
      font-size: 16px;
      color: #333;
      line-height: 56px;
      position: relative;
      user-select: none;

      @m open {
        color: #999;
      }

      a {
        color: #333;
        display: block;
        user-select: none;
        padding-left: 20px;
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);

        &:active {
          background: #ECECEC;
        }

        > p {
          border-top: 1px solid #e5e5e5;
        }
      }

      .van-icon-arrow {
        position: absolute;
        font-size: 12px;
        line-height: 1;
        top: 24px;
        right: 20px;
      }
    }

    @e list-wrapper {
      height: 0;
      overflow: hidden;

      @m open {
        height: auto;
      }
    }

    @e list {
      transform: translateY(-50%);
      transition: transform .2s ease-out;

      @m open {
        transform: translateY(0);
      }
    }

    li {
      list-style: none;
    }

    ul {
      padding: 0;
      margin: 0;
      overflow: hidden;
    }
  }
}

</style>
