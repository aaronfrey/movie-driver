<template>
    <div>
        <h1>Movie Search</h1>
        <hr>
        <form>

            <section>
                <h2>Rating</h2>
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <label for="rating">Rating</label>
                            <select class="custom-select custom-select-lg" id="rating">
                                <option value="ALL" selected>All Ratings</option>
                                <option v-for="rating in this.ratings" :key="rating.id" :value="rating.rating">
                                    {{ rating.rating }}
                                </option>
                            </select>
                        </div>
                    </div>
                </div>
            </section>

            <section>
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
            </section>

            <button type="submit" class="btn btn-lg btn-primary">Submit</button>

        </form>

    </div>

</template>

<script>
    export default {
        data: function() {
            return {
                ratings: [],
                showReleaseDateRange: false
            }
        },
        methods: {
            getRatings: function() {
                axios.get('/api/ratings')
                    .then(res => {
                        this.ratings = res.data;
                    }).catch(err => {
                    console.log(err);
                });
            },
            toggleReleaseDateRange: function() {
                this.showReleaseDateRange = !this.showReleaseDateRange;
            }
        },
        mounted() {
            console.log('Movie Search Form mounted.');
            this.getRatings();
        }
    }
</script>
