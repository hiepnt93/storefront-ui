<template>
  <div id="my-account">
    <SfBreadcrumbs
      class="breadcrumbs desktop-only"
      :breadcrumbs="breadcrumbs"
    />
    <SfContentPages
      title="My Account"
      :active="activePage"
      class="my-account"
      @click:change="changeActivePage"
    >
      <SfContentCategory title="Personal Details">
        <SfContentPage title="My profile">
          <MyProfile
            :account="account"
            @update:personal="account = { ...account, ...$event }"
            @update:password="account = { ...account, ...$event }"
          />
        </SfContentPage>
        <SfContentPage title="Shipping details">
          <ShippingDetails
            :account="account"
            @update:shipping="account = { ...account, ...$event }"
          />
        </SfContentPage>
        <SfContentPage title="Loyalty Card">
          <LoyaltyCard />
        </SfContentPage>
        <SfContentPage title="My newsletter">
          <MyNewsletter />
        </SfContentPage>
      </SfContentCategory>
      <SfContentCategory title="Order details">
        <SfContentPage title="Order history">
          <OrderHistory :account="account" />
        </SfContentPage>
        <SfContentPage title="My reviews">
          <MyReviews />
        </SfContentPage>
      </SfContentCategory>
      <SfContentPage title="Log out" />
    </SfContentPages>
  </div>
</template>
<script>
import { SfBreadcrumbs, SfContentPages } from "@storefront-ui/vue";
import {
  MyProfile,
  ShippingDetails,
  LoyaltyCard,
  MyNewsletter,
  OrderHistory,
  MyReviews
} from "./_internal/index.js";

export default {
  name: "MyAccount",
  components: {
    SfBreadcrumbs,
    SfContentPages,
    MyProfile,
    ShippingDetails,
    LoyaltyCard,
    MyNewsletter,
    OrderHistory,
    MyReviews
  },
  data() {
    return {
      activePage: "My profile",
      breadcrumbs: [
        {
          text: "Home",
          route: {
            link: "#"
          }
        },
        {
          text: "My Account",
          route: {
            link: "#"
          }
        }
      ],
      account: {
        firstName: "Sviatlana",
        lastName: "Havaka",
        email: "example@email.com",
        password: "a*23Et",
        shipping: [
          {
            firstName: "Sviatlana",
            lastName: "Havaka",
            streetName: "Zielinskiego",
            apartment: "24/193A",
            city: "Wroclaw",
            state: "Lower Silesia",
            zipCode: "53-540",
            country: "Poland",
            phoneNumber: "(00)560 123 456"
          },
          {
            firstName: "Sviatlana",
            lastName: "Havaka",
            streetName: "Zielinskiego",
            apartment: "20/193A",
            city: "Wroclaw",
            state: "Lower Silesia",
            zipCode: "53-603",
            country: "Poland",
            phoneNumber: "(00)560 123 456"
          }
        ],
        orders: [
          ["#35765", "4th Nov, 2019", "Visa card", "$12.00", "In process"],
          ["#35766", "4th Nov, 2019", "Paypal", "$12.00", "Finalised"],
          ["#35768", "4th Nov, 2019", "Mastercard", "$12.00", "Finalised"],
          ["#35769", "4th Nov, 2019", "Paypal", "$12.00", "Finalised"]
        ]
      }
    };
  },
  methods: {
    changeActivePage(title) {
      if (title === "Log out") {
        alert("You are logged out!");
        return;
      }
      this.activePage = title;
    }
  }
};
</script>
<style lang="scss" scoped>
@import "~@storefront-ui/vue/styles";

#my-account {
  box-sizing: border-box;
  @include for-desktop {
    max-width: 1240px;
    margin: 0 auto;
  }
}
.breadcrumbs {
  padding: var(--spacer-big) var(--spacer-extra-big) var(--spacer-extra-big)
    var(--spacer-extra-big);
}
</style>
