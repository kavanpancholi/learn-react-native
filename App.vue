<template>
    <app-navigation></app-navigation>
</template>

<script>
import { StackNavigator } from "vue-native-router";
import HomeScreen from "./Home";
import DetailScreen from "./Detail";
const AppNavigation = StackNavigator(
    {
        Home: HomeScreen,
        Details: DetailScreen
    },
    {
        initialRouteName: "Home"
    }
);
export default {
    components: { AppNavigation }
};
</script>