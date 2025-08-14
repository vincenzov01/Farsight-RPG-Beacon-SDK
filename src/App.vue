<script setup>
import { useAppStore } from '@/stores/index.js'
import { useMetaStore } from '@/stores/metaStore.js'
import { useSheetStore } from '@/stores/sheetStore.js'

// These stores should drive how to access the data in your sheet, and how to trigger actionable events.
const appStore = useAppStore()
// The meta store has generic character info for every sheet.
const meta = useMetaStore()
// The sheet store is where you want to be to customize what data / fields are on your sheet.
const sheet = useSheetStore()
</script>
<template>
  <div class="header">
    <div class="title">Quickstart Sheet</div>
    <button class="button" @click="appStore.loadExampleData">Reset</button>
  </div>
  <div class="sheet">
    <div class="card">
      <div class="avatar">
        <img :src="meta.avatar" alt="Character Avatar" />
      </div>
      <label for="character_name">
        <span class="label">Character Name</span>
      </label>
      <input id="character_name" v-model="meta.name" />
      <label for="faction">
        <span class="label">Faction</span>
      </label>
      <input id="faction" v-model="sheet.faction" />
    </div>
    <div class="card">
      <div class="subheader">
        <div class="subtitle">Traits - {{ sheet.traitsCount }}</div>
        <button class="button" @click="sheet.addTrait">Add</button>
      </div>
      <div class="traits">
        <div class="trait-item" v-for="trait in sheet.traits" :key="trait._id">
          <input v-model="trait.name" placeholder="Name" />
          <input v-model="trait.description" placeholder="Description" />
          <button class="button" @click="sheet.postTraitToChat(trait)">Chat</button>
          <button class="button" @click="sheet.removeTrait(trait._id)">Remove</button>
        </div>
      </div>
    </div>
  </div>
</template>