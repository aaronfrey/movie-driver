<template>
    <div>
        <h1>Movie Search</h1>
        <hr>
        <form>

            <section>
                <h2>Rating</h2>
                <div class="form-row">
                    <div class="col">
                        <div class="form-group">
                            <div class="btn-group btn-group-lg btn-group-toggle">
                                <label class="btn btn-drive" :class="{ active: selectedRating === 'ALL' }">
                                    <input type="radio" value="ALL" v-model="selectedRating" autocomplete="off" checked> All
                                </label>
                                <label v-for="rating in this.ratings" :key="rating.id"
                                    class="btn btn-drive" :class="{ active: selectedRating === rating }">
                                    <input type="radio" :value="rating" v-model="selectedRating" autocomplete="off"> {{ rating.rating }}
                                </label>
                            </div>
                        </div>
                        <div class="alert alert-drive">
                            <span v-if="selectedRating !== 'ALL'">{{ selectedRating.description }}</span>
                            <span v-else>Search will include all movie ratings.</span>
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

            <button type="submit" class="btn btn-lg btn-drive">Submit</button>

        </form>

    </div>

</template>

<script>
    export default {
        data: function() {
            return {
                ratings: [],
                selectedRating: 'ALL',
                showReleaseDateRange: false
            }
        },
        methods: {
            getRatings() {
                axios.get('/api/ratings').then(res => {
                    this.ratings = res.data;
                }).catch(err => {
                    console.log(err);
                });
            },
            toggleReleaseDateRange() {
                this.showReleaseDateRange = !this.showReleaseDateRange;
            }
        },
        created() {
            this.getRatings();
        },
        mounted() {
            console.log('Movie Search Form mounted.');
        }
    }
</script>
