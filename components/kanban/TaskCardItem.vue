<template>
  <v-card
    max-width=400
  >
    <v-card-title>
      <v-list-item class="grow">
        <v-row
            align="center"
          >
          <v-chip
            class="ma-2"
            color=primary
            label
            text-color="white"
          >
            <v-icon left>mdi-alpha-{{ ticketType }}-box-outline</v-icon>
            {{ ticketId }}
          </v-chip>
          <v-chip
            class="ma-2"
            color="red"
            v-for="tag in tags"
            :key="tag"
          >
            {{ tag }}
          </v-chip>
        </v-row>
      </v-list-item>
    </v-card-title>

    <v-card-text class="headline font-weight-bold">
      {{ ticketTitle }}
    </v-card-text>

    <v-card-actions>
      <v-list-item class="grow">
        <v-tooltip bottom>
          <template v-slot:activator="{ on }">
          <v-avatar v-on="on">
            <v-img
              :alt="assignee.name"
              :src="assignee.avatar"
             ></v-img>
          </v-avatar>
          </template>
         <span>{{ assignee.name }}</span>
        </v-tooltip>

        <v-spacer></v-spacer>

        <v-row
          align="center"
          justify="end"
        >
          <v-menu
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="dateRange"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
             <template v-slot:activator="{ on }">
              <v-text-field
                v-model="dateRangeText"
                label="Date début et fin"
                readonly
                clearable
                v-on="on"
                @click:clear="dateRange = []"
               ></v-text-field>
             </template>
            <v-date-picker v-model="dateRange" no-title range>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="menu = false">Annuler</v-btn>
              <v-btn text color="primary" @click="$refs.menu.save(dateRange)">OK</v-btn>
            </v-date-picker>
          </v-menu>
          <span class="mr-1 ml-1">·</span>
          <v-menu
            ref="menu1"
            v-model="menu1"
            :close-on-content-click="false"
            :return-value.sync="estimation"
            transition="scale-transition"
            offset-y
            min-width="290px"
          >
            <template v-slot:activator="{ on }">
              <v-btn icon color="pink" v-on="on">
                <v-icon class="mr-1">mdi-clock-outline</v-icon>
              </v-btn>
            </template>
           <v-card>
             <v-card-text>
              <v-text-field
                label="Estimation"
                prepend-inner-icon="schedule"
                outlined
                v-model="estimation"
                clearable
                ></v-text-field>
            </v-card-text>
            <v-divider />
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn text color="primary" @click="menu1 = false">Annuler</v-btn>
              <v-btn text color="primary" @click="$refs.menu1.save(estimation)">OK</v-btn>
            </v-card-actions>
           </v-card>
          </v-menu>
          <span class="subheading">{{ estimation }}h</span>
        </v-row>
      </v-list-item>
    </v-card-actions>
  </v-card>
</template>

<script>

export default {
  data() {
    return {
      ticketId: 15966,
      ticketTitle : 'Enquête - Script : changer icônes',
      ticketType: 'd',
      tags : ['Critique', 'Demo'],
      assignee: {
        name: 'Naris Razafimahatratra',
        avatar: 'https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light'
      },
      dateRange: ['2020-04-19', '2020-04-19'],
      estimation: 8,
      menu: false,
      menu1: false,
      modal: false,
    }
  },
  computed: {
    dateRangeText () {
      return this.dateRange
        .map(date => this.$moment(date).format('ll'))
        .join(' ~ ')
    },
  },
}

</script>