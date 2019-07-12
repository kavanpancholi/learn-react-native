<template>
    <view class="container">
        <scroll-view>
            <view>
                <scroll-view :horizontal="true">
                    <image
                        :style="{width: navigation.getParam('width'), height: navigation.getParam('height')}"
                        :source="{uri: unEntity(navigation.getParam('photo'))}"
                    />
                </scroll-view>
                <touchable-opacity class="button" :on-press="onPressButton">
                    <text class="button-text">Go Back</text>
                </touchable-opacity>
            </view>
        </scroll-view>
    </view>
</template>
<script>
export default {
    props: {
        navigation: {
            type: Object
        }
    },
    methods: {
        onPressButton: function() {
            this.navigation.goBack();
        },
        unEntity: function(str) {
            return str.replace(/&amp;/g, "&");
        }
    }
};
</script>
<style>
.container {
    background-color: white;
    align-items: center;
    justify-content: center;
    flex: 1;
}
.button {
    background-color: #333;
    padding: 10px;
}
.button-text {
    color: #fff;
}
</style>
