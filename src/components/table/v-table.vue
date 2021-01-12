<template>
    <div class="v-table">
        <div class="v-table__header">
            <p @click="sortByName">Name 
                <i class="material-icons">unfold_more</i>
                </p>
            <p @click="sortByPointsEarned">Points earned 
                <i class="material-icons">unfold_more</i>
                </p>
            <p @click="sortByPointsSpent">Points spent 
                <i class="material-icons">unfold_more</i>
                </p>
            <p @click="sortByRegistrationDate">Registration date 
                <i class="material-icons">unfold_more</i>
                </p>
        </div>
        <div class="v-table__body">
            <v-table-row 
            :row_data="row"
            v-for="row in paginatedUsers"
            :key="row.id"
            />
        </div>
        <div class="v-table__pagination">
            <div class="page" 
            v-for="(page, index) in pages"
            :key="index"
            :class="{page__selected: page === pageNumber}"
            @click="pageClick(page)"
            >
                {{page}}
            </div>
        </div>
    </div>
</template>

<script>
import vTableRow from './v-table-row'
export default {
    name: 'v-table',
    props: {
        users_data: {
            type: Array,
            default: () => {
                return []
            }
        }
    },
    data(){
        return {
            usersPerPage: 10,
            pageNumber: 1
        }
    },
    components: {
        vTableRow
    },
    computed: {
        pages(){
            return Math.ceil(this.users_data.length / 10);
        },
        paginatedUsers(){
            let from = (this.pageNumber - 1) * this.usersPerPage;
            let to = from + this.usersPerPage;
            return this.users_data.slice(from, to);
        }
    },
    methods: {
        pageClick(page){
            this.pageNumber = page;
        },
        sortByName(){
            this.users_data.sort((a,b) => a.name.localeCompare(b.name))
        },
        sortByPointsEarned(){
            this.users_data.sort((a,b) => a.points_earned - b.points_earned)
        },
        sortByPointsSpent(){
            this.users_data.sort((a,b) => a.points_spent - b.points_spent)
        },
        sortByRegistrationDate(){
            this.users_data.sort((a,b) => a.registration_date.localeCompare(b.registration_date))
        },

    }
}
</script>

<style scoped>
.v-table{
    max-width: 900px;
    margin: 0 auto;
}
    .v-table__header{
        display: flex;
        justify-content: space-around;
        align-items: center;
        border-bottom: 1px solid grey;
    }
    .v-table__header p{
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-basis: 25%;
        text-align: left;
        padding: 8px 16px;
        font-weight: bold;
        cursor: pointer;
    }
    .v-table__pagination{
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-top: 30px;
    }
    .page{
        cursor: pointer;
        padding: 8px;
        border: 1px solid grey;
        margin-right: 4px;
    }
    .page:hover{
        background: lightgreen;
    }
    .page__selected{
        background: lightgreen;
        border: 1px solid grey;
    }

</style>