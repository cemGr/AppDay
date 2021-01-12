<template>
    <Page>
        <ActionBar title="Home" />


        <ScrollView>
            <StackLayout class="home-panel">
                <!--Add your page content here-->
                <Label textWrap="true" text="heyy!"
                    class="h2 description-label" />
                <Label textWrap="true"
                    text="Write code in the editor or drag and drop components to build a NativeScript mobile application."
                    class="h2 description-label" />
                <Label textWrap="true"
                    text="Scan the QR code with your mobile device and watch the changes sync live while you play with the code."
                    class="h2 description-label" />
            </StackLayout>
        </ScrollView>
        <StackLayout>
            <BottomNavigation height="400px">
                <TabStrip>
                    <TabStripItem>
                        <Label text="News"></Label>
                        <Image src="res://home"></Image>
                    </TabStripItem>
                    <TabStripItem>
                        <Label text="Events"></Label>
                        <Image src="res://settings"></Image>
                    </TabStripItem>
                    <TabStripItem>
                        <Label text="Map"></Label>
                        <Image src="res://browse"></Image>
                    </TabStripItem>
                    <TabStripItem>
                        <Label text="Info"></Label>
                        <Image src="res://favorites"></Image>
                    </TabStripItem>
                </TabStrip>
                <TabContentItem>

                    <ListView for="department in departments"
                        @itemTap="onItemTap">
                        <v-template>
                            <FlexboxLayout flexDirection="row">
                                <Image :src="department.imageSrc"
                                    class="thumb img-circle" />
                                <Label :text="department.name" class="t-12"
                                    style="width: 60%" />
                            </FlexboxLayout>
                        </v-template>
                    </ListView>
                </TabContentItem>
                <TabContentItem>
                    <ListView for="feed in feeds">
                        <v-template>
                            <StackLayout height="350">
                                <Image :src="feed.image" height="300"
                                    stretch="aspectFill" />
                                <Label :text="feed.title" class="h2" />
                            </StackLayout>
                        </v-template>
                    </ListView>
                </TabContentItem>
                <TabContentItem>
                    <WebView :src="encodeURI(url1)" />
                </TabContentItem>
                <TabContentItem>
                    <StackLayout orientation="vertical">
                        <Image height="25%" class="m-t-30"
                            src="https://upload.wikimedia.org/wikipedia/en/thumb/1/1c/HKBU_Logo.svg/316px-HKBU_Logo.svg.png" />
                        <Label class="m-t-20 h1 text-center"
                            text="HKBU InfoDay App" />

                        <FlexboxLayout flexWrap="wrap"
                            flexDirection="row-reverse" class="m-30 h2"
                            height="240">
                            <Label text="1" backgroundColor="#EEEEEE"
                                flexGrow="1" />
                            <Label text="2" backgroundColor="#DDDDDD"
                                flexGrow="2" />
                            <Label text="3" backgroundColor="#003BF9"
                                flexGrow="3" />
                            <Label text="Medical Clinic: 3411-7447"
                                backgroundColor="#BBBBBB" flexGrow="4" />
                            <Label text="Emergencies: 3411-7777"
                                backgroundColor="#AAAAAA" flexGrow="5" />
                            <Label text="Admission Office: 3411-2200"
                                backgroundColor="#999999" flexGrow="6" />
                        </FlexboxLayout>
                    </StackLayout>
                </TabContentItem>
            </BottomNavigation>
        </StackLayout>
    </Page>
</template>

<script>
    export default {
        methods: {
            onItemTap: function(args) {
                console.log("Item with index: " + args.index + " tapped");
            }
        },

        async mounted() {
            var response = await fetch(global.baseUrl +
                "/256da2ee7badc12b0ec2");
            if (response.ok) {
                this.feeds = await response.json();
                console.log(JSON.stringify(this.feeds));
            } else {
                console.log(response.statusText);
            }
        },

        data() {
            return {
                feeds: [],
                departments: [{
                        name: "Computer Science",
                        imageSrc: "https://cslinux0.comp.hkbu.edu.hk/~mtchoy/comp_logo.png"
                    },
                    {
                        name: "Communication_Studies",
                        imageSrc: "https://cslinux0.comp.hkbu.edu.hk/~mtchoy/comm_logo.png"
                    }
                ],

                url1: "https://leaflet-api.vercel.app?center=22.34,114.18&zoom=17&marker=AC Hall|22.341072,114.179645&sensor="
            };
        }
    };
</script>

<style scoped>
    .home-panel {
        vertical-align: center;
        font-size: 20;
        margin: 15;
    }

    .description-label {
        margin-bottom: 15;
    }
</style>