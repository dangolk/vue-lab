<template>
    <div class="card mt-5"> 
        <h2 class="card-header">{{header}}</h2> 
        <transition name="shooting-star"> 
            <div class="mt-3 ml-3" v-cloak v-if="numAsteroids > 0 && showSummary"> 
                <p>showing {{numAsteroids}} items</p> 
                <p>{{closestObject}} has the smallest miss distance.</p> 
            </div> 
        </transition> 
        <div class="m-3"> 
            <a href="#" @click="showSummary = !showSummary">Show/hide summary</a> 
        </div> 
        <table class="table table-striped" :class="[{'table-dark': false}, 'table-bordered']"> 
            <thead class="thead-light"> 
                <th>#</th> 
                <th>Name</th> 
                <th>Close Approach Date</th> 
                <th>Miss Distance</th> 
                <th>Remove</th> 
            </thead> 
            <tbody is="transition-group" name="neo-list" v-cloak> 
                <tr v-for="(a, index) in asteroids" 
                    :key="a.neo_reference_id" 
                    :class="{highlight: isMissingData(a), 'shadow-sm': true}"> 
                    <td>{{index + 1}}</td> 
                    <td>{{a.name}}</td> 
                    <td>{{getCloseApproachDate(a)}}</td> 
                    <td> 
                        <ul v-if="a.close_approach_data.length > 0"> 
                            <li v-for="(value, key) in a.close_approach_data[0].miss_distance"> 
                                {{key}}: {{value}} 
                            </li> 
                        </ul> 
                    </td> 
                    <td><button class="btn btn-warning" @click="remove(index)">remove</button></td> 
                </tr> 
            </tbody> 
        </table> 
    </div>
</template>

<script>
    export default {

    }
</script>

<style>

</style>