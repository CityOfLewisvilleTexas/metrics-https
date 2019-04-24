<template>
<div>
    <h3 slot="title">Look here</h3>
    <form-helper>
        <p slot="text">Hello</p>
    </form-helper>
        <div>
            <p>{{ title }}</p>
            <img src="" alt=""/>
            <button @click="snapshot()">load snapshot</button>
        </div>
</div>
</template>

<script>
import formHelper from '../widgets/FormHelper.vue'
export default {
    components: {
        'form-helper': formHelper
    },
    data() {
        return {
            title: ''
        }
    },
    methods: {
         snapshot() {
           axios.get('https://www.googleapis.com/pagespeedonline/v1/runPagespeed?screenshot=true&strategy=mobile&url=https://lewisville.maps.arcgis.com/apps/opsdashboard/index.html#/c29f1923a2b94cd7881ef87f2bb3b34f').then(function(response) {
                return response;
            })
            .then(function(myJson) {
              let screenshot = myJson.data.screenshot
				app.title = screenshot
				console.log(screenshot)

				 var imageData = screenshot.data.replace(/_/g, "/").replace(/-/g, "+");
          // Build the Data URI.
          var dataURI = "data:" + screenshot.mime_type + ";base64," + imageData;
          // Set the image's source.
          console.log(dataURI)
			document.querySelector('img').setAttribute('src', dataURI)
            });
        }
    },
    created: {

    },
    mounted: {
       
    },
    updated: {

    },
    beforeDestroy:{

    }

}
</script>

<style scoped>

</style>
