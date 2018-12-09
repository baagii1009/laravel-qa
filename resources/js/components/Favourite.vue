<template>
<<<<<<< HEAD
    <a 
        title="Click to mark as favourite model (Click again to undo)" 
        :class="classes"        
        @click.prevent="toggle"
    >
        <i class="fas fa-star fa-2x"></i>
        <span class="favourites-count">
            {{ count }}
        </span>
    </a>
</template>

<script>
    export default {
        props: ['question'],
        data() {
            return {
                isFavourited: this.question.is_favourited,
                count: this.question.favourites_count,
                id: this.question.id
            }
        },
        computed: {
            classes(){
                return [
                    'favourite',
                    'mt-2',
                    !this.signedIn ? 'off' : (this.isFavourited ? 'favourited' : '')
                ];
            },
            endpoint() {
                return `/questions/${this.id}/favourites`;
            },
            signedIn() {
                return window.Auth.signedIn;
            }
        },
        methods: {
            toggle() {
                if (!this.signedIn) {
                    this.$toast.warning(
                        "Please login to favourite this question",
                        "Warning",
                        {
                            timeout: 3000,
                            position: 'bottomLeft'
                        }
                    );
                    return;
                }
                this.isFavourited ? this.destroy() : this.create();
            },
            destroy() {
                axios.delete(this.endpoint)
                .then(res => {
                    this.count--;
                    this.isFavourited = false;                    
                });
            },
            create() {
                axios.post(this.endpoint)
                .then(res => {
                    this.count++;
                    this.isFavourited = true;

                });
            }
        }
    }
=======
    <a title="Click to mark as favorite question (Click again to undo)" 
        :class="classes" @click.prevent="toggle">
        <i class="fas fa-star fa-2x"></i>
        <span class="favorites-count">{{ count }}</span>
    </a>
</template>
<script>
export default {
    props: ['question'],
    data () {
        return {
            isFavorited: this.question.is_favorited,
            count: this.question.favorites_count,            
            id: this.question.id
        }
    },
    computed: {
        classes () {
            return [
                'favorite', 'mt-2',
                ! this.signedIn ? 'off' : (this.isFavorited ? 'favorited' : '')
            ];
        },
        endpoint () {
            return `/questions/${this.id}/favorites`;
        },
        signedIn () {
            return window.Auth.signedIn;
        }
    },
    methods: {
        toggle () {
            if (! this.signedIn) {
                this.$toast.warning("Please login to favorite this question", "Warning", {
                    timeout: 3000,
                    position: 'bottomLeft'
                });
                return;
            }
            this.isFavorited ? this.destroy() : this.create();
        },
        destroy () {
            axios.delete(this.endpoint)
            .then(res => {
                this.count--;
                this.isFavorited = false;
            });
        },
        create () {
            axios.post(this.endpoint)
            .then(res => {
                this.count++;
                this.isFavorited = true;
            });
        }
    }
}
>>>>>>> lesson-33
</script>