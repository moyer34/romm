<script setup>
import { ref, inject } from 'vue'
import { downloadRom, downloadSave } from '@/services/download.js'

// Props
const props = defineProps(['rom'])
const saveFiles = ref(false)

// Event listeners bus
const emitter = inject('emitter')
</script>

<template>
    <v-card-text>
        <v-row>
            <v-col class="pa-0">
                <v-btn
                    @click="downloadRom(rom, emitter)"
                    icon="mdi-download"
                    size="x-small"
                    variant="text"/>
                <v-btn
                    @click="downloadSave(rom, emitter)"
                    icon="mdi-content-save-all"
                    size="x-small"
                    variant="text"
                    :disabled="!saveFiles"/>
            </v-col>

            <v-menu location="bottom">
                <template v-slot:activator="{ props }">
                    <v-btn
                        @click=""
                        v-bind="props"
                        icon="mdi-dots-vertical"
                        size="x-small"
                        variant="text"
                        disabled/>
                </template>
                <v-list rounded="0" class="pa-0">
                    <v-list-item @click="searchRomIGDB()" class="pt-4 pb-4 pr-5">
                        <v-list-item-title class="d-flex"><v-icon icon="mdi-search-web" class="mr-2"/>Search IGDB</v-list-item-title>
                    </v-list-item>
                    <v-divider class="border-opacity-25"/>
                    <v-list-item @click="dialogEditRom=true" class="pt-4 pb-4 pr-5">
                        <v-list-item-title class="d-flex"><v-icon icon="mdi-pencil-box" class="mr-2"/>Edit</v-list-item-title>
                    </v-list-item>
                    <v-divider class="border-opacity-25"/>
                    <v-list-item @click="dialogDeleteRom=true" class="pt-4 pb-4 pr-5 text-red">
                        <v-list-item-title class="d-flex"><v-icon icon="mdi-delete" class="mr-2"/>Delete</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>
        </v-row>
    </v-card-text>
</template>