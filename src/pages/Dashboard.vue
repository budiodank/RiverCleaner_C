<template>
  <div class="content">
    <div class="md-layout" v-for="tool_detail in tools_detail">
      <!-- Box of Content -->
        <div class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-25" @click="detail(tool_detail.tools_id)">
          <stats-card data-background-color="blue">
            <template slot="header">
              <md-icon>opacity</md-icon>
            </template>

            <template slot="content">
              <p class="category">Power of Hydrogen</p>
              <h3 class="title">{{ tool_detail.ph }}</h3>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>date_range</md-icon>
                Last updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </stats-card>
        </div>
        <div class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-25" @click="detailWaste(tool_detail.tools_id)">
          <stats-card data-background-color="green">
            <template slot="header">
              <md-icon>restore_from_trash</md-icon>
            </template>

            <template slot="content">
              <p class="category">Weight Waste</p>
              <h3 class="title">
                {{ tool_detail.weight }} / {{ tool_detail.ttlWaste }}
                <small>grams</small>
              </h3>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>date_range</md-icon>
                Last updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </stats-card>
        </div>
        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-25"
        >
          <stats-card data-background-color="orange">
            <template slot="header">
              <md-icon>refresh</md-icon>
            </template>

            <template slot="content">
              <p class="category">Waste Transported</p>
              <h3 class="title">{{ tool_detail.transported }}
                <small>times</small>
              </h3>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>date_range</md-icon>
                Last updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </stats-card>
        </div>

        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-25"
        >
          <stats-card data-background-color="red">
            <template slot="header">
              <md-icon>info_outline</md-icon>
            </template>

            <template slot="content">
              <p class="category">Waste Not Transported</p>
              <h3 class="title">{{ tool_detail.cnt_transported }}
                <small>times</small>
              </h3>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>date_range</md-icon>
                Last updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </stats-card>
        </div>
      <!-- Chart -->
        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
        >
          <chart-card
            :chart-data="sensorPhChart.data"
            :chart-options="sensorPhChart.options"
            :chart-type="'Line'"
            data-background-color="blue"
          >
            <template slot="content">
              <h4 class="title">Sensor PH</h4>
              <p class="category" @click="detail(tool_detail.tools_id)">
                Rata-Rata PH Per-Jam
              </p>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>access_time</md-icon>
                updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </chart-card>
        </div>
        <!--<div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-33"
        >
          <chart-card
            :chart-data="emailsSubscriptionChart.data"
            :chart-options="emailsSubscriptionChart.options"
            :chart-responsive-options="emailsSubscriptionChart.responsiveOptions"
            :chart-type="'Bar'"
            data-background-color="red"
          >
            <template slot="content">
              <h4 class="title">Email Subscription</h4>
              <p class="category">
                Last Campaign Performance
              </p>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>access_time</md-icon>
                updated 10 days ago
              </div>
            </template>
          </chart-card>
        </div>-->
        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
        >
          <chart-card
            :chart-data="sensorLoadChart.data"
            :chart-options="sensorLoadChart.options"
            :chart-type="'Line'"
            data-background-color="green"
          >
            <template slot="content">
              <h4 class="title">Weight Waste</h4>
              <p class="category" @click="detailWaste(tool_detail.tools_id)">
                Rata-Rata Waste Per-Jam
              </p>
            </template>

            <template slot="footer">
              <div class="stats">
                <md-icon>access_time</md-icon>
                updated 
                  <div v-if="tool_detail.hours === '0'"></div>
                  <div v-else-if="tool_detail.hours !== '0'">{{ tool_detail.hours }} hour </div> 
                {{ tool_detail.minutes }} minutes ago
              </div>
            </template>
          </chart-card>
        </div>
        <!-- Table -->
        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
        >
          <md-card>
            <md-card-header data-background-color="blue">
              <h4 class="title">Data Sensor</h4>
              <p class="category">Data Normal</p>
            </md-card-header>
            <md-card-content>
              <ph-table table-header-color="blue"></ph-table>
            </md-card-content>
          </md-card>
        </div>

        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
        >
          <md-card>
            <md-card-header data-background-color="red">
              <h4 class="title">Data Sensor</h4>
              <p class="category">Data Problem</p>
            </md-card-header>
            <md-card-content>
              <ph-table-problem table-header-color="red"></ph-table-problem>
            </md-card-content>
          </md-card>
        </div>
        <!--
        <div
          class="md-layout-item md-medium-size-100 md-xsmall-size-100 md-size-50"
        >
          <nav-tabs-card>
            <template slot="content">
              <span class="md-nav-tabs-title">Tasks:</span>
              <md-tabs class="md-success" md-alignment="left">
                <md-tab id="tab-home" md-label="Bugs" md-icon="bug_report">
                  <nav-tabs-table></nav-tabs-table>
                </md-tab>

                <md-tab id="tab-pages" md-label="Website" md-icon="code">
                  <nav-tabs-table></nav-tabs-table>
                </md-tab>

                <md-tab id="tab-posts" md-label="server" md-icon="cloud">
                  <nav-tabs-table></nav-tabs-table>
                </md-tab>
              </md-tabs>
            </template>
          </nav-tabs-card>
        </div>
        -->
    </div>
  </div>
</template>

<script>
import {
  StatsCard,
  ChartCard,
  NavTabsCard,
  NavTabsTable,
  OrderedTable,
  PhTable,
  PhTableProblem
} from "@/components";

export default {
  components: {
    StatsCard,
    ChartCard,
    NavTabsCard,
    NavTabsTable,
    OrderedTable,
    PhTable,
    PhTableProblem
  },
  data() {
    return {
      phHour: [],
      wasteHour: [],
      sensorPhChart: {
        data: {
          labels: [],
          series: []
        },
        options: {
          lineSmooth: this.$Chartist.Interpolation.cardinal({
            tension: 0
          }),
          low: 0,
          high: 12, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 0
          }
        }
      },
      sensorLoadChart: {
        data: {
          /*labels: ["12am", "3pm", "6pm", "9pm", "12pm", "3am", "6am", "9am"],
          series: [[230, 750, 450, 300, 280, 240, 200, 190]]*/
          labels: [],
          series: []
        },

        options: {
          lineSmooth: this.$Chartist.Interpolation.cardinal({
            tension: 0
          }),
          low: 100,
          high: 1000, // creative tim: we recommend you to set the high sa the biggest value + something for a better look
          chartPadding: {
            top: 0,
            right: 0,
            bottom: 0,
            left: 0
          }
        }
      },
      /*emailsSubscriptionChart: {
        data: {
          labels: [
            "Ja",
            "Fe",
            "Ma",
            "Ap",
            "Mai",
            "Ju",
            "Jul",
            "Au",
            "Se",
            "Oc",
            "No",
            "De"
          ],
          series: [[542, 443, 320, 780, 553, 453, 326, 434, 568, 610, 756, 895]]
        },
        options: {
          axisX: {
            showGrid: false
          },
          low: 0,
          high: 1000,
          chartPadding: {
            top: 0,
            right: 5,
            bottom: 0,
            left: 0
          }
        },
        responsiveOptions: [
          [
            "screen and (max-width: 640px)",
            {
              seriesBarDistance: 5,
              axisX: {
                labelInterpolationFnc: function(value) {
                  return value[0];
                }
              }
            }
          ]
        ]
      },*/
      errorMessage : "",
      successMessage : "",
      tools_detail: [],
      tools_detail_hour: []
      //labelsHour: [],
    };
  },
  mounted: function () {
    console.log("Test getSumTools");
    this.getToolsDetail();
    this.getToolsHour();
  },
  methods: {
    detail (id) {
      this.$router.push('tools/detailph/'+id)
    },
    detailWaste (id) {
      this.$router.push('tools/detailwaste/'+id)
    },
    getToolsDetail: function(){
      let currentObj = this;

      let config = {
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/x-www-form-urlencoded'
        },
      }

      this.axios.get("http://api.inoprex.com/include/tools_detail.php?action=sum", config)
      .then(function(response){
        console.log(response.data.tools_detail);
        if (response.data.error) {
          currentObj.errorMessage = response.data.message;
        }else{
          currentObj.tools_detail = response.data.tools_detail;
        }
      });
    },
    getToolsHour: function(){
      let currentObj = this;

      let config = {
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/x-www-form-urlencoded'
        },
      }

      this.axios.get("http://api.inoprex.com/include/tools_detail.php?action=hour", config)
      .then(function(response){
        console.log(response.data.tools_detail_hour);
        if (response.data.error) {
          currentObj.errorMessage = response.data.message;
        }else{
          currentObj.tools_detail_hour = response.data.tools_detail_hour;
          response.data.tools_detail_hour.map(function(value, key) {
            currentObj.sensorPhChart.data.labels.push(value.hours);
            currentObj.sensorLoadChart.data.labels.push(value.hours);
            currentObj.phHour.push(value.ph);
            currentObj.wasteHour.push(value.weight);
          });
          currentObj.sensorLoadChart.data.series.push(currentObj.wasteHour);
          currentObj.sensorPhChart.data.series.push(currentObj.phHour);
            
          //currentObj.sensorPhChart.data.labels = response.data.tools_detail_hour.hours;
          //console.log("currentObj.sensorPhChart.data.labels : "+currentObj.sensorPhChart.data.labels);
          //currentObj.sensorPhChart.data.series = response.data.tools_detail_hour.ph;
        }
      });
    }
  }
};
</script>
