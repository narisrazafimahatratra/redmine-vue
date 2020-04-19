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
        <v-list-item-avatar color="grey darken-3">
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
        </v-list-item-avatar>

        <v-row
          align="center"
          justify="end"
        >
          <v-icon class="mr-1">mdi-calendar-arrow-right</v-icon>
          <span class="subheading mr-2">{{ $moment(startDate).format("ll") }}</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1">mdi-calendar-arrow-left</v-icon>
          <span class="subheading mr-2">{{ $moment(endDate).format("ll") }}</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1">mdi-progress-check</v-icon>
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
      startDate: '04-05-2020',
      endDate: '04-05-2020',
      estimation: 8
    }
  }
}

</script>