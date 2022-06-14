<template>
<div>
    <!-- <h1>HI sdfgdskl;glfdskgdsk;lgkjf;llk</h1>
    <v-menu
        eager
        relative
        float
        :close-on-content-click="false"
        :key="reRender"
        :nudge-bottom="44"
        ref="gidsearchbarmenu"
        transition="slide-y-transition"
        content-class="gid-search-dropdown elevation-0"
        style="min-height: 383px"
    >
    <template #activator="{ on }">
    <v-text-field
        v-on="on"
        flat
        solo
        dense
        rounded
        :autofocus="!isTopbar"
        hide-details
        ref="searchBox"
        :label="placeholder"
        :title="placeholder"
        :disabled="disabled"
        v-model="searchTextModel"
        :placeholder="barFocused || !isTopbar ? placeholder : 'Search'"
        class="ml-2 text-field"
        :class="
        focused || isSearch
            ? 'search-txt-flexible-expanded'
            : 'search-txt-flexible'
        "
        @input="onTextAdded"
        @keyup.enter="onEnterClick()"
        @keydown.stop="handleKeydown"
        @click.stop="toggleMenuBar(true)"
        @focus.stop="onSearchFocus"
        @blur.stop="onSearchBlur"
    >
    </v-text-field>
    </template>

    <div
    v-if="!doShowNoResult && (suggestions.length || length)"
    :key="reRender"
    @mouseenter="
        onMeta = true;
        barFocused = true;
        focused = true;
    "
    > -->
    <!-- <SearchSuggestions
        @on-suggestion-click="handleSuggestionClick"
        @on-filter-click="handleFilterClick"
        :facets="facets"
        :flag="flag"
        :length="length"
        :suggestions="suggestions"
        :suggestionHeader="getSuggestionHeader"
        :isTopbar="isTopbar"
    >
    </SearchSuggestions> -->
    <!-- </div>
    </v-menu> -->
</div>
</template>

<script>
export default{
    name: 'gidSearchBox',
    data(){
        
    },
    
}
</script>

<style>
</style>