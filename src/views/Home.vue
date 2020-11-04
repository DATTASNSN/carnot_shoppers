<template>
  <v-container class="home" fluid>
    <v-container fluid>
      <v-card
        color="#10164A"
      >
        <v-card-text
          class="white--text text-h5 text-center"
        >
          {{ groceryTitle }}
        </v-card-text>
      </v-card>
      <br>
      <v-card
        color="#10164A"
      >
        <v-card-text>
          <v-row
            justify="center"
            align="center"
          >
            <v-chip
              class="text-center white--text ma-3"
              color="#EF5350"
              label
            >
              <b>Organization of {{ groceryOrg }} Government</b>
            </v-chip>
          </v-row>
          <br>
          <v-card
            color="#262C49"
          >
            <v-row
              justify="center"
              align="center"
            >
              <v-chip
                class="text-center white--text ma-3"
                color="#EF5350"
                label
              >
                <b>Types Of Organizations</b>
              </v-chip>
            </v-row>
            <v-row>
              <v-col
                v-for="(groceryType, i) in groceryTypeOrg"
                :key="i"
              >
                <v-chip
                  class="text-center white--text ma-3"
                  color="#42A5F5"
                  label
                >
                  <b>Organization of {{ groceryType }} Government</b>
                </v-chip>
              </v-col>
            </v-row>
          </v-card>
          <br>
          <v-card
            color="#262C49"
          >
            <v-row
              justify="center"
              align="center"
            >
              <v-chip
                  class="text-center white--text ma-3"
                  color="#EF5350"
                  label
                >
                  <b>Types Of Sectors</b>
                </v-chip>
            </v-row>
            <v-row
              justify="center"
              align="center"
            >
              <v-col
                v-for="(grocerySec, i) in grocerySector"
                :key="i"
                cols="12"
                lg="2"
                md="1"
                sm="2"
              >
                <v-chip
                  class="text-center white--text ma-3"
                  color="#42A5F5"
                  label
                >
                  <b>{{ grocerySec }}</b>
                </v-chip>
              </v-col>
            </v-row>
          </v-card>
        </v-card-text>
      </v-card>
      <br>
      <v-data-iterator
        :items="groceryList"
        :search="search"
        :items-per-page.sync="groceryList.length"
        :sort-desc="sortDesc"
        :sort-by="sortBy.toLowerCase()"
        light
        hide-default-footer
      >
        <template v-slot:header>
          <v-row align="center" justify="end">
            <v-col cols="12" md="4" sm="12" xs="12">
              <v-toolbar
                color="transparent"
                flat
                class="mb-3"
              >
                <v-select
                  v-model="sortBy"
                  class="ma-2"
                  flat
                  solo-inverted
                  hide-details
                  :items="keys"
                  background-color="#F8BBD0"
                  append-icon="fas fa-angle-down"
                  label="Sort by"
                ></v-select>
                <v-text-field
                  v-model="search"
                  class="ma-2"
                  clearable
                  hide-details
                  solo
                  background-color="#F8BBD0"
                  append-icon="fas fa-search"
                  label="Search"
                ></v-text-field>
              </v-toolbar>
            </v-col>
          </v-row>
        </template>
        <template v-slot:default="props">
          <v-card
            color="#10164A"
          >
            <v-row>
              <v-col
                v-for="(grocery) in props.items"
                :key="grocery"
                cols="12"
                lg="3"
                md="6"
                sm="12"
              >
                <v-container>
                  <v-card
                    color="#7986CB"
                    class="text-center"
                  >
                    <v-card-text
                      class="text-center text-title font-weight-bold white--text"
                      color="#5E35B1"
                      label
                    >
                      TimeStamp : {{ grocery.timestamp }}
                    </v-card-text>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      State : {{ grocery.state }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      District : {{ grocery.district }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Commodity : {{ grocery.commodity }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Variety : {{ grocery.variety }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Arrival Date : {{ grocery.arrival_date }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Minimum Price : {{ grocery.min_price }}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Max Price : {{ grocery.max_price}}
                    </v-chip>
                    <br>
                    <v-chip
                      class="text-center white--text ma-3 chip-width"
                      color="#5E35B1"
                      label
                    >
                      Modal Price : {{ grocery.modal_price }}
                    </v-chip>
                  </v-card>
                </v-container>
              </v-col>
            </v-row>
          </v-card>
        </template>
      </v-data-iterator>
    </v-container>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Home',
  data() {
    return {
      search: '',
      sortDesc: true,
      sortBy: 'arrival_date',
      keys: [
        'arrival_date',
        'max_price',
        'min_price',
        'modal_price',
      ],
      groceryList: [],
      groceryTitle: '',
      grocerySector: [],
      groceryOrg: '',
      groceryTypeOrg: [],
      groceryTypeField: [],
    };
  },
  mounted() {
    axios.get('https://api.data.gov.in/resource/9ef84268-d588-465a-a308-a864a43d0070?api-key=579b464db66ec23bdd000001cdd3946e44ce4aad7209ff7b23ac571b&format=json&offset=0&limit=10')
      .then(this.setGrocerylist)
      .catch();
  },
  methods: {
    setGrocerylist(response) {
      console.log(response.data.records);
      this.groceryList = response.data.records;
      this.groceryTitle = response.data.title;
      this.grocerySector = response.data.sector;
      this.groceryOrg = response.data.org_type;
      this.groceryTypeOrg = response.data.org;
      this.groceryTypeField = response.data.field;
    },
  },
  computed: {
    filteredKeys() {
      return this.keys.filter((key) => key !== 'arrival_date');
    },
  },
};
</script>

<style>
.chip-width {
  width: 250px !important;
}
</style>
