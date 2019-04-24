<template>
	<div class="text-xs-center">
      <v-container>
        <v-layout justify-center>
          <v-flex xs8>
            <v-card v-model="currentMetric">
              <v-card-text v-for="(metric, index) in metrics" :key="index" :id="index">
				  <div v-if="metric.metricname" :class="{ static: metric.metrictype.toLowerCase() === 'static', dynamic: metric.metrictype.toLowerCase() != 'static' }">
                <h5>Metric # {{ index + 1 }} : {{ metric.metricname }}</h5>
                    <p v-if="metric.Department"><b>Department: </b>{{ metric.Department }}</p>
                    <p v-if="metric.metricdescription != null"><b>Description: </b>{{ metric.metricdescription }}</p>
                    <p v-if="metric.url"><b>URL Information:</b> {{ metric.urllabel }} <span :class="{ link: metric.url != null }"><a :href="metric.url" target="_blank">{{ metric.url }}</a></span></p>
                    <p v-if="metric.psofia_createddate"><b>Created Date:</b>{{ formatDate(metric.psofia_createddate) }}</p>
                    <p v-if="metric.psofia_editeddate"><b> Date Last Edited: </b>{{ formatDate(metric.psofia_editeddate) }}</p>
            	</div>
              </v-card-text>
            </v-card>
			 <v-pagination color="#512da8" :length="currentMetric" v-model="currentMetric" totalVisible="20"></v-pagination>
          </v-flex>
        </v-layout>
      </v-container>
    </div>
</template>

<script>
import moment from 'moment'
import Vuetify from 'vuetify'

export default {
	name: 'ExampleWidget',
	components: {
	},
	props: {
		metrics: {
			type: Array,
			required: true
		},
		pages: {
			type: Number,
			required: true
		},
		currentMetric: {
			type: Number,
			required:true
		}
	},
	data () {
		return {
			
		}
	},

	computed: {

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
        formatDate: function(date) {
            if(date) {
                return moment(date).format("dddd, MMMM Do YYYY, h:mm:ss a")
            }
            else {
                return 'No date listed'
             }
		},
		nextPage() {
			this.currentPage++
		},
		previousPage() {
			this.currentPage--
		}
	}
}
</script>

<!-- anything here only applies to this component (because of "scoped") -->
<style scoped>

.link::before {
    content: "("
}
a {
    text-decoration: underline;
    color:rgb(0, 89, 255);
    font-size: 1rem;
    cursor:pointer;
}
.link::after {
    content: ")"
}

div {
    border-top: 1px solid #dedede;
}

div:first-child {
    border-top: none;
}

.theme--light.v-pagination .v-pagination__item--active {
    color: #fff;
    background-color: #512da8;
}

</style>
