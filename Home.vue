<template>
    <view class="container">
        <text class="text-color-primary">Reddit EarthPorn Wallpapers</text>
        <scroll-view>
            <view class="image-container">
                <view class="image" v-for="(photo, index) in photos" :key="index">
                    <touchable-opacity :on-press="() => photoClicked(photo)">
                        <image
                            :style="{height:dimentions.height,width: dimentions.width}"
                            :source="{uri: photo.data.thumbnail}"
                        />
                    </touchable-opacity>
                </view>
            </view>
        </scroll-view>
    </view>
</template>
<script>
import { Dimensions } from "react-native";
export default {
    props: {
        navigation: {
            type: Object
        }
    },
    data() {
        return {
            photos: []
        };
    },
    computed: {
        dimentions() {
            const dimensions = Dimensions.get("window");
            const imageWidth = (dimensions.width / 100) * 50;
            const imageHeight = 140;
            return { height: imageHeight, width: imageWidth };
        }
    },
    mounted() {
        fetch("https://www.reddit.com/r/EarthPorn.json")
            .then(response => response.json())
            .then(data => {
                this.photos = data.data.children;
            });
    },
    methods: {
        photoClicked(photo) {
            const length = photo.data.preview.images[0].resolutions.length;
            this.navigation.navigate("Details", {
                photo: photo.data.preview.images[0].resolutions[length - 1].url,
                width:
                    photo.data.preview.images[0].resolutions[length - 1].width,
                height:
                    photo.data.preview.images[0].resolutions[length - 1].height
            });
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
.text-color-primary {
    background-color: #333;
    color: #fff;
    font-size: 24px;
    text-align: center;
    width: 100%;
    padding: 15px;
}
.button {
    background-color: #333;
    padding: 10px;
}
.button-text {
    color: #fff;
}
.image-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: wrap;
}
</style>
