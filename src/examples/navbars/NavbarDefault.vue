<script setup>
import { RouterLink } from "vue-router";
import { ref, watch } from "vue";
import { useWindowsWidth } from "../../assets/js/useWindowsWidth";

// images
import ArrDark from "@/assets/img/down-arrow-dark.svg";
import downArrow from "@/assets/img/down-arrow.svg";
import DownArrWhite from "@/assets/img/down-arrow-white.svg";

const props = defineProps({
  action: {
    type: Object,
    route: String,
    color: String,
    label: String,
    default: () => ({
      route: "https://www.creative-tim.com/product/vue-material-kit",
      color: "bg-gradient-success",
      label: "Free Download"
    })
  },
  transparent: {
    type: Boolean,
    default: false
  },
  light: {
    type: Boolean,
    default: false
  },
  dark: {
    type: Boolean,
    default: false
  },
  sticky: {
    type: Boolean,
    default: false
  },
  darkText: {
    type: Boolean,
    default: false
  }
});

// set arrow  color
function getArrowColor() {
  if (props.transparent && textDark.value) {
    return ArrDark;
  } else if (props.transparent) {
    return DownArrWhite;
  } else {
    return ArrDark;
  }
}

// set text color
const getTextColor = () => {
  let color;
  if (props.transparent && textDark.value) {
    color = "text-dark";
  } else if (props.transparent) {
    color = "text-white";
  } else {
    color = "text-dark";
  }

  return color;
};

// set nav color on mobile && desktop

let textDark = ref(props.darkText);
const { type } = useWindowsWidth();

if (type.value === "mobile") {
  textDark.value = true;
} else if (type.value === "desktop" && textDark.value == false) {
  textDark.value = false;
}

watch(
  () => type.value,
  (newValue) => {
    if (newValue === "mobile") {
      textDark.value = true;
    } else {
      textDark.value = false;
    }
  }
);
</script>
<template>
  <nav class="navbar navbar-expand-lg top-0" :class="{
    'z-index-3 w-100 shadow-none navbar-transparent position-absolute my-3':
      props.transparent,
    'my-3 blur border-radius-lg z-index-3 py-2 shadow py-2 start-0 end-0 mx-4 position-absolute mt-4':
      props.sticky,
    'navbar-light bg-white py-3': props.light,
    ' navbar-dark bg-gradient-dark z-index-3 py-3': props.dark
  }">
    <div :class="
      props.transparent || props.light || props.dark
        ? 'container'
        : 'container-fluid px-0'
    ">
      <RouterLink class="navbar-brand d-none d-md-block" :class="[
        (props.transparent && textDark.value) || !props.transparent
          ? 'text-dark font-weight-bolder ms-sm-3'
          : 'text-white font-weight-bolder ms-sm-3'
      ]" :to="{ name: 'presentation' }" rel="tooltip" title="Designed and Coded by Creative Tim"
        data-placement="bottom">
        野麓YELU CAMP
      </RouterLink>
      <RouterLink class="navbar-brand d-block d-md-none" :class="
        props.transparent || props.dark
          ? 'text-white'
          : 'font-weight-bolder ms-sm-3'
      " to="/" rel="tooltip" title="Designed and Coded by Creative Tim" data-placement="bottom">
        Material Design
      </RouterLink>
      <a href="https://www.creative-tim.com/product/vue-material-kit-pro"
        class="btn btn-sm bg-gradient-success mb-0 ms-auto d-lg-none d-block">Buy Now</a>
      <button class="navbar-toggler shadow-none ms-2" type="button" data-bs-toggle="collapse" data-bs-target="#navigation"
        aria-controls="navigation" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon mt-2">
          <span class="navbar-toggler-bar bar1"></span>
          <span class="navbar-toggler-bar bar2"></span>
          <span class="navbar-toggler-bar bar3"></span>
        </span>
      </button>





      <div class="collapse navbar-collapse w-100 pt-3 pb-2 py-lg-0" id="navigation">
        <ul class="navbar-nav navbar-nav-hover ms-auto">
          <!-- 導覽列第一個按鈕 -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a role="button" class="nav-link ps-2 d-flex cursor-pointer align-items-center" :class="getTextColor()"
              id="dropdownMenuBlocks" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="material-icons opacity-6 me-2 text-md" :class="getTextColor()">view_day</i>
              營區預定
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-2 d-lg-block d-none" />
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-1 d-lg-none d-block ms-auto" />
            </a>
            <div
              class="dropdown-menu dropdown-menu-end dropdown-menu-animation dropdown-md dropdown-md-responsive p-3 border-radius-lg mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuBlocks">
              <div class="d-none d-lg-block">
                <ul class="list-group">
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md" href="javascript:;">
                      <div class="d-flex">
                        <div class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6
                              class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                              北部
                            </h6>
                            <span class="text-sm">See all sections</span>
                          </div>
                          <img :src="downArrow" alt="down-arrow" class="arrow" />
                        </div>
                      </div>
                    </a>
                    <div class="dropdown-menu mt-0 py-3 px-2 mt-3">
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-headers' }">
                        新北
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-features' }">
                        桃園
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-features' }">
                        新竹
                      </RouterLink>
                    </div>
                  </li>
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md" href="javascript:;">
                      <div class="d-flex">
                        <div class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6
                              class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                              中部
                            </h6>
                            <span class="text-sm">See all navigations</span>
                          </div>
                          <img :src="downArrow" alt="down-arrow" class="arrow" />
                        </div>
                      </div>
                    </a>
                    <div class="dropdown-menu mt-0 py-3 px-2 mt-3">
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'navigation-navbars' }">
                        苗栗
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'navigation-navtabs' }">
                        南投
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1"
                        :to="{ name: 'navigation-pagination' }">
                        台中
                      </RouterLink>
                    </div>
                  </li>
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md" href="javascript:;">
                      <div class="d-flex">
                        <div class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6
                              class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                              南部
                            </h6>
                            <span class="text-sm">See all input areas</span>
                          </div>
                          <img :src="downArrow" alt="down-arrow" class="arrow" />
                        </div>
                      </div>
                    </a>
                    <div class="dropdown-menu mt-0 py-3 px-2 mt-3">
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-inputs' }">
                        嘉義
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-forms' }">
                        台南
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-forms' }">
                        高雄
                      </RouterLink>
                    </div>
                  </li>
                  <li class="nav-item dropdown dropdown-hover dropdown-subitem list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md" href="javascript:;">
                      <div class="d-flex">
                        <div class="w-100 d-flex align-items-center justify-content-between">
                          <div>
                            <h6
                              class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                              東部
                            </h6>
                            <span class="text-sm">See all examples</span>
                          </div>
                          <img :src="downArrow" alt="down-arrow" class="arrow" />
                        </div>
                      </div>
                    </a>
                    <div class="dropdown-menu mt-0 py-3 px-2 mt-3">
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-alerts' }">
                        宜蘭
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-modals' }">
                        花蓮
                      </RouterLink>
                      <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-tooltips-popovers' }">
                        台東
                      </RouterLink>
                    </div>
                  </li>
                </ul>
              </div>
              <!-- 以下是為了設定RWD -->
              <div class="row d-lg-none">
                <div class="col-md-12">
                  <div class="d-flex mb-2">
                    <div class="w-100 d-flex align-items-center justify-content-between">
                      <div>
                        <h6
                          class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                          北部
                        </h6>
                      </div>
                    </div>
                  </div>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-headers' }">
                    新北
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-features' }">
                    桃園
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'page-features' }">
                    新竹
                  </RouterLink>
                  <div class="d-flex mb-2 mt-3">
                    <div class="w-100 d-flex align-items-center justify-content-between">
                      <div>
                        <h6
                          class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                          中部
                        </h6>
                      </div>
                    </div>
                  </div>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'navigation-navbars' }">
                    苗栗
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'navigation-navtabs' }">
                    南投
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'navigation-pagination' }">
                    台中
                  </RouterLink>
                  <div class="d-flex mb-2 mt-3">
                    <div class="w-100 d-flex align-items-center justify-content-between">
                      <div>
                        <h6
                          class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                          南部
                        </h6>
                      </div>
                    </div>
                  </div>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-inputs' }">
                    嘉義
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-forms' }">
                    台南
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'inputareas-forms' }">
                    高雄
                  </RouterLink>
                  <div class="d-flex mb-2 mt-3">
                    <div class="w-100 d-flex align-items-center justify-content-between">
                      <div>
                        <h6
                          class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                          東部
                        </h6>
                      </div>
                    </div>
                  </div>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-alerts' }">
                    宜蘭
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-modals' }">
                    花蓮
                  </RouterLink>
                  <RouterLink class="dropdown-item ps-3 border-radius-md mb-1" :to="{ name: 'ac-tooltips-popovers' }">
                    台東
                  </RouterLink>
                </div>
              </div>
            </div>
          </li>


          <!-- 導覽列第二個按鈕 -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a role="button" class="nav-link ps-2 d-flex cursor-pointer align-items-center" :class="getTextColor()"
              id="dropdownMenuPages" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="material-icons opacity-6 me-2 text-md" :class="getTextColor()">dashboard</i>
              當地活動
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-2 d-lg-block d-none" />
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-1 d-lg-none d-block ms-auto" />
            </a>
            <div class="dropdown-menu dropdown-menu-animation ms-n3 dropdown-md p-3 border-radius-xl mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuPages">
              <div class="row d-none d-lg-block">
                <div class="col-12 px-4 py-2">
                  <div class="row">
                    <div class="position-relative">
                      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-1">
                        北部
                      </div>
                      <!-- test -->
                      <RouterLink :to="{ name: 'test' }" class="dropdown-item border-radius-md">
                        <span>Test</span>
                      </RouterLink>
                      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-1">
                        中部
                      </div>
                      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-1">
                        南部
                      </div>
                      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-1">
                        東部
                      </div>

                      <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-0 mt-3">
                        Account
                      </div>
                      <RouterLink :to="{ name: 'signin-basic' }" class="dropdown-item border-radius-md">
                        <span>Sign In</span>
                      </RouterLink>

                    </div>
                  </div>
                </div>
              </div>


              <!-- 以下是為了設定RWD -->
              <div class="d-lg-none">
                <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-0">
                  Landing Pages
                </div>
                <RouterLink :to="{ name: 'about' }" class="dropdown-item border-radius-md">
                  <span>About Us</span>
                </RouterLink>
                <RouterLink :to="{ name: 'contactus' }" class="dropdown-item border-radius-md">
                  <span>Contact Us</span>
                </RouterLink>
                <RouterLink :to="{ name: 'author' }" class="dropdown-item border-radius-md">
                  <span>Author</span>
                </RouterLink>
                <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-0 mt-3">
                  Account
                </div>
                <RouterLink :to="{ name: 'signin-basic' }" class="dropdown-item border-radius-md">
                  <span>Sign In</span>
                </RouterLink>
              </div>
            </div>
          </li>


          <!-- 導覽列第三個按鈕 -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a role="button" class="nav-link ps-2 d-flex cursor-pointer align-items-center" :class="getTextColor()"
              id="dropdownMenuDocs" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="material-icons opacity-6 me-2 text-md" :class="getTextColor()">article</i>
              行程挑選
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-2 d-lg-block d-none" />
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-1 d-lg-none d-block ms-auto" />
            </a>
            <div
              class="dropdown-menu dropdown-menu-end dropdown-menu-animation dropdown-md mt-0 mt-lg-3 p-3 border-radius-lg"
              aria-labelledby="dropdownMenuDocs">
              <div class="d-none d-lg-block">
                <ul class="list-group">
                  <li class="nav-item list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md"
                      href=" https://www.creative-tim.com/learning-lab/vue/overview/material-kit/">
                      <h6
                        class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                        自選行程
                      </h6>
                      <span class="text-sm">All about overview, quick start, license and
                        contents</span>
                    </a>
                  </li>
                  <li class="nav-item list-group-item border-0 p-0">
                    <a class="dropdown-item py-2 ps-3 border-radius-md"
                      href=" https://www.creative-tim.com/learning-lab/vue/colors/material-kit/">
                      <h6
                        class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                        套裝行程
                      </h6>
                      <span class="text-sm">See our colors, icons and typography</span>
                    </a>
                  </li>
                </ul>
              </div>

              <!-- 以下是為了設定RWD -->
              <div class="row d-lg-none">
                <div class="col-md-12 g-0">
                  <a class="dropdown-item py-2 ps-3 border-radius-md" href="./pages/about-us.html">
                    <h6
                      class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                      自選行程
                    </h6>
                    <span class="text-sm">All about overview, quick start, license and
                      contents</span>
                  </a>
                  <a class="dropdown-item py-2 ps-3 border-radius-md" href="./pages/about-us.html">
                    <h6
                      class="dropdown-header text-dark font-weight-bolder d-flex justify-content-cente align-items-center p-0">
                      套裝行程
                    </h6>
                    <span class="text-sm">See our colors, icons and typography</span>
                  </a>
                </div>
              </div>
            </div>
          </li>

          <!-- 導覽列第四個按鈕 -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a role="button" class="nav-link ps-2 d-flex cursor-pointer align-items-center" :class="getTextColor()"
              id="dropdownMenuPages" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="material-icons opacity-6 me-2 text-md" :class="getTextColor()">dashboard</i>
              露營商店
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-2 d-lg-block d-none" />
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-1 d-lg-none d-block ms-auto" />
            </a>
            <div class="dropdown-menu dropdown-menu-animation ms-n3 dropdown-md p-3 border-radius-xl mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuPages">
              <div class="row d-none d-lg-block">
                <div class="col-12 px-4 py-2">
                  <div class="row">
                    <div class="position-relative">
                      <RouterLink :to="{ name: 'about' }" class="dropdown-item border-radius-md">
                        <span>About Us</span>
                      </RouterLink>
                      <RouterLink :to="{ name: 'contactus' }" class="dropdown-item border-radius-md">
                        <span>Contact Us</span>
                      </RouterLink>

                    </div>
                  </div>
                </div>
              </div>
              <!-- 以下是為了設定RWD -->
              <div class="d-lg-none">
                <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-0">
                  露營商店
                </div>
                <RouterLink :to="{ name: 'about' }" class="dropdown-item border-radius-md">
                  <span>About Us</span>
                </RouterLink>
                <RouterLink :to="{ name: 'contactus' }" class="dropdown-item border-radius-md">
                  <span>Contact Us</span>
                </RouterLink>
              </div>
            </div>
          </li>


          <!-- 導覽列第五個按鈕 -->
          <li class="nav-item dropdown dropdown-hover mx-2">
            <a role="button" class="nav-link ps-2 d-flex cursor-pointer align-items-center" :class="getTextColor()"
              id="dropdownMenuPages" data-bs-toggle="dropdown" aria-expanded="false">
              <i class="material-icons opacity-6 me-2 text-md" :class="getTextColor()">dashboard</i>
              登入/註冊
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-2 d-lg-block d-none" />
              <img :src="getArrowColor()" alt="down-arrow" class="arrow ms-1 d-lg-none d-block ms-auto" />
            </a>
            <div class="dropdown-menu dropdown-menu-animation ms-n3 dropdown-md p-3 border-radius-xl mt-0 mt-lg-3"
              aria-labelledby="dropdownMenuPages">
              <div class="row d-none d-lg-block">
                <div class="col-12 px-4 py-2">
                  <div class="row">
                    <div class="position-relative">
                      <RouterLink :to="{ name: 'about' }" class="dropdown-item border-radius-md">
                        <span>會員中心</span>
                      </RouterLink>
                      <RouterLink :to="{ name: 'contactus' }" class="dropdown-item border-radius-md">
                        <span>註冊新會員</span>
                      </RouterLink>

                    </div>
                  </div>
                </div>
              </div>
              <!-- 以下是為了設定RWD -->
              <div class="d-lg-none">
                <div class="dropdown-header text-dark font-weight-bolder d-flex align-items-center px-0">
                  登入/註冊
                </div>
                <RouterLink :to="{ name: 'about' }" class="dropdown-item border-radius-md">
                  <span>會員中心</span>
                </RouterLink>
                <RouterLink :to="{ name: 'contactus' }" class="dropdown-item border-radius-md">
                  <span>註冊新會員</span>
                </RouterLink>
              </div>
            </div>
          </li>



        </ul>
      </div>
    </div>
  </nav>
  <!-- End Navbar -->
</template>
