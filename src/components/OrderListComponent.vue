<template>
    <v-container>
            <v-row>
                <v-col>
                <v-card>
                    <v-card-title class="text-center text-h5">
                        주문목록
                    </v-card-title>
                    <v-card-text>
                        <v-data-table
                        :headers="tableHeaders"
                        :items = "orderList"
                        class = "elevation-1"
                        show-expand
                        >
                        <template v-slot:[`item.actions`]="{item}">
                            <v-btn v-if="item.orderStatus ==='ORDERED'">
                                CANCEL
                            </v-btn>
                        </template>
                        <template v-slot:expanded-row="{item}">
                            <v-row>
                                <v-col>
                                    <v-list-item v-for="orderItem in item.orderDetails">
                                        <v-list-item-content>
                                            <v-list-item-title>
                                                
                                            </v-list-item-title>
                                        </v-list-item-content>
                                    </v-list-item>
                                </v-col>
                            </v-row>
                        </template>
                        </v-data-table>
                    </v-card-text>
                </v-card>
            </v-col>
            </v-row>
            </v-container>
</template>
<script>
import axios from 'axios';

export default{
    data(){
        return{
            tableHeaders:[{title:"ID",key:'id',align:'start'},
            {title:"회원 EMAIL",key:'memberEmail',align:'start'},
            {title:"주문상태",key:'orderStatus',align:'start'},
            {title:"ACTION",key:'actions',align:'start'}
            ],
            orderList:[]
        }
    },
    async created(){
        const response = await axios.get(`${process.env.VUE_APP_API_BASE_URL}/ordering/list`);
        this.orderList = response.data;
    },
    methods:{

    }
}
</script>