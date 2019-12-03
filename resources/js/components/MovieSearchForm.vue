<template>
    <div>
        <h1>Movie Search</h1>
        <hr>
        <form >
            <div class="d-flex justify-content-between align-items-end">
                <h2>Release Year</h2>
                <div class="custom-control custom-switch">
                    <input type="checkbox" class="custom-control-input" id="release-year-range"
                        @click="toggleReleaseDateRange()">
                    <label class="custom-control-label" for="release-year-range">Search Release Range</label>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col-md-4">
                    <label for="release-year">Release Year</label>
                    <input type="text" class="form-control form-control-lg" id="release-year"
                        :disabled="showReleaseDateRange">
                </div>
                <div class="form-group col-md-4">
                    <label for="release-year-min">Release Year GTE</label>
                    <input type="text" class="form-control form-control-lg" id="release-year-min"
                        :disabled="!showReleaseDateRange">
                </div>
                <div class="form-group col-md-4">
                    <label for="release-year-max">Release Year LTE</label>
                    <input type="text" class="form-control form-control-lg" id="release-year-max"
                        :disabled="!showReleaseDateRange">
                </div>
            </div>
            <button type="submit" class="btn btn-lg btn-primary">Submit</button>
        </form>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                showReleaseDateRange: false
            }
        },
        methods: {
            toggleReleaseDateRange: function() {
                this.showReleaseDateRange = !this.showReleaseDateRange;
            }
        },
        mounted() {
            console.log('Movie Search Form mounted.')
        }
    }
</script>
