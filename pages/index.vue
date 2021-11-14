<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div v-if="!authUser">
        <Top />
      </div>
      <div v-else>
        <Home />
        <!-- <Backup /> -->
      </div>
    </v-col>
  </v-row>
</template>
