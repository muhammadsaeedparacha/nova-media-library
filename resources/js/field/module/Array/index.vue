<template>
    <div>
        <draggable
            :class="'flex flex-wrap space-x-3 nml-display-' + type"
            v-if="array && array.length"
            item-key="id"
            v-model="array"
            @end="changeArray(array)"
            :disabled="!isForm"
        >
            <template #item="{ element }">
                <!-- <div class="nml-item"> -->
                    <!-- <div class="relative w-32">
                        <div class="title truncate text-center" v-text="element.title || element.name" />
                        <img class="h-40 w-32" :src="element.url" />
                        // <button v-if="isForm" @click="remove(i)">Remove</button>
                    </div> -->
                    <a :href="element.url" target="_blank" class="no-underline">
                        <img class="block rounded-lg shadow-md max-w-xs"
                            v-if="`image` === mime(element)"
                            :src="element.preview || element.url"
                            :alt="__('This file could not be found')" />

                        <div v-else>
                            <div class="nml-item relative mb-2 cursor-pointer" :title="element.title || element.name">

                            <div :class="'icon rounded-lg shadow-md nml-icon-'+mime(element)" :style="bg(element)" />

                            <div class="title truncate" v-text="element.title || element.name" />
                            <svg v-if="isForm" class="delete shadow-md dim" @click.stop="remove(i)"><icon-delete/></svg>
                            </div>
                        </div>
                    </a>
            </template>


        </draggable>

        <div
            class="card border-lg border-50 max-w-xs cursor-pointer border p-8 text-center"
            v-else-if="isForm"
            @click="popup = true"
        >
            {{ __('Select Files') }}
        </div>

        <div class="mt-4 space-x-5" v-if="isForm && array && array.length">
            <a class="dim text-primary-500 inline-block cursor-pointer font-bold" @click="popup = true">
                {{ __('Media Library') }}
            </a>

            <a class="dim text-red-500 ml-8 inline-block cursor-pointer font-bold" @click="changeArray([])">
                {{ __('Clear') }}
            </a>
        </div>

        <transition name="fade" mode="out-in">
            <Library v-if="popup" isArray :field="field" />
        </transition>
    </div>
</template>

<script src="./script.js"></script>
