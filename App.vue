<template>
  <div id="app">

    <!-- Navigation -->
    <nav class="navigation">   
      <ul>
        <li 
          v-for="page in pages" 
          :key="page"
          @click="setActivePage(page)"
          :style="getActiveState(page)">
          <button data-ico="⛺" class="custom-button">{{ page }}</button>
        </li>
      </ul>
    </nav>

    <!-- Actual page -->
    <br>

    <MainPage v-if="activePage == pages[0]" @setactivepage="setActivePage"/>
    <LogInPage v-if="activePage == pages[1]"/>
    <SignUpPage v-if="activePage == pages[2]"/>
    <BookingPage v-if="activePage == pages[3]"/>
    <BookingCancelPage v-if="activePage == pages[4]"/>
    <BookingOverviewPage v-if="activePage == pages[5]"/>
    <UserInformationPage v-if="activePage == pages[6]"/>
    <OwnerLoginPage v-if="activePage == pages[7]"/>
    <OwnerAddSpotPage v-if="activePage == pages[9]"/>

  </div>
</template>

<script>
import LogInPage from './Views/LogInPage.vue';
import MainPage from './Views/MainPage.vue';
import SignUpPage from './Views/SignUpPage.vue';
import BookingPage from "./Views/BookingPage.vue";
import BookingCancelPage from "./Views/BookingCancelPage.vue";
import BookingOverviewPage from "./Views/BookingOverviewPage.vue";
import UserInformationPage from "./Views/UserInformationPage.vue";
import OwnerLoginPage from './components/OwnerLoginPage.vue';
import OwnerAddSpotPage from './components/OwnerAddSpotPage.vue';


export default {
  name: 'App',
  components: {
    MainPage,
    LogInPage,
    SignUpPage,
    BookingPage,
    BookingCancelPage,
    BookingOverviewPage,
    UserInformationPage,
    OwnerLoginPage,
    OwnerAddSpotPage,
 
  },
  data() {
    return {
      pages: [
        "Main",
        "LogIn",
        "SignUp",
        "Booking",
        "Booking Cancel",
        "Booking Overview",
        "User Information Change",
        "Owner login",
      
      ],
      activePage: "Main"
    }
  },
  methods: {
    setActivePage(page) {
      this.activePage = page;
    },
    getActiveState(page) {
      if (this.activePage == page) {
        return "text-decoration: underline";
      }
    }
  }
}
</script>

<style>
/* Navigation styles */
.navigation {
  background-color: #33abc1;
  background: linear-gradient(to right bottom, #00efe7, #0453f1) border-box;
  padding: 20px;
}

.navigation ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.navigation li {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
  color: #13175a;
}

/* Button styles */
button.custom-button {
  display: flex;
  align-items: center;
  justify-content: center;
  border: solid 0.2em transparent;
  padding: 0.5em 1em;
  border-radius: 1.5em;
  background: linear-gradient(to right bottom, var(--primary-color), var(--secondary-color)) border-box;
  font: 700 1em/1 ubuntu, sans-serif;
  text-transform: uppercase;
  position: relative;
  color: var(--text-color); /* Ensure the text is visible */
}



button.custom-button::after { 
  content: attr(data-ico);
  margin-left: 0.5em; /* Add space between text and emoji */
  color: var(--icon-color); /* Ensure the icon is visible */
}

.navigation li.active {
  text-decoration: underline;
}
</style>
