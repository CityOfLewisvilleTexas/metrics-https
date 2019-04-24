<template>
	<div v-if="!isLoading">
	  <div id="logo__banner">
          <img src="static/pmartin.svg" width="100px;"/>
             <h1>{{ message }} {{ metrics }}</h1>
             <h5>There are currently <span v-if="returnAllMetrics.length > 0" class="active" :class="{ plus: returnAllMetrics.length > 100, medium: returnAllMetrics.length < 100 & returnAllMetrics.length > 50, low: returnAllMetrics.length < 50}">{{ returnAllMetrics.length }}</span> active metrics</h5>
    </div>
         <GoogleMap :config="config" :id="config.compid"></GoogleMap>
            <div>
            <ExampleWidget 
            :metrics="returnAllMetrics" 
            :pages="returnAllMetrics.length"
            :currentMetric="sortedMetrics"></ExampleWidget>
            </div>
            <div>{{ sortedMetrics }}</div>
	</div>
</template>

<script>
import ExampleWidget from '@/components/widgets/ExampleWidget'
import GoogleMap from '@/components/widgets/GoogleMap'

export default {
	name: 'Example',
	components: {
        ExampleWidget,
        GoogleMap
	},
    props: [],
	data () {
		return {
            message: 'Basic Metrics Information',
            config: {
                compid: 'traffic',
                why: 'Just Generic stuff here!',
                title: 'Current Travel Conditions'
            } 
		}
	},

	computed: {
        returnAllMetrics: function() {
            return this.$store.state.metrics
        },
        isLoading: function() {
			return this.$store.state.isLoading
        },
        sortedMetrics: function() {
            return this.$store.state.metrics.sort(function(a, b) {
                    return a.index > b.index ? 1 : -1 
            })
        }
        },

	watch: {
	},

	// START HERE
	mounted() {
      
	},

	// called as component is removed
	beforeDestroy() {
	},

	methods: {
	}
}
</script>

<!-- anything here only applies to this component (because of "scoped") -->
<style scoped>

* {
    font-family:'Product Sans', sans-serif;
    color: black;
    text-align: left;
    margin:5px;
    padding:5px;
}

.active {
     border: 1px solid #fefefe;
    border-radius: 50px;
    padding:10px 8px;
}

.active.plus {
    color:#fff;
    font-weight:700;
    background-color: rgb(15, 161, 22);
}

.active.medium {
    color:#090909;
    font-weight:700;
    background-color: rgb(241, 188, 14);
    border: 1px solid #fefefe;
    border-radius: 25px;
    padding:8px;
}

.active.low {
    color:#090909;
    font-weight:700;
    background-color: rgb(241, 40, 14);
    border: 1px solid #fefefe;
    border-radius: 25px;
    padding:8px;
}

#logo__banner {
    background-color: #512da8 !important;
    margin:0 0 12px 0;
    
}

#logo__banner > img {
    background-color: inherit;
    display: inline-block;
}

#logo__banner > h1 {
    color: #fff; 
    background-color: inherit;
    margin-top: 0;
      display: inline-block;
      vertical-align: text-bottom;
}

#logo__banner > h5 {
    color: #fff; 
    background-color: inherit;
    margin-left:25px;
    margin-bottom: 12px;
}

#traffic {
    height: 340px;
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 65%;
}

</style>
