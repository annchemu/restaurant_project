<template>
    <v-container>
        <v-card color="blue" >
            <v-card-title>
                <div class="text-h3">Our Menu</div>
            </v-card-title>
        </v-card>
    </v-container>
    <!-- Array -->
    <v-container>
        <v-card class="mx-auto" elevation="24">
            <v-container>
                <v-row>
                    <v-col cols="12" md="4" v-for="item in menuItems" :key=item>
                        <v-card color="yellow">
                            <v-card-item>
                            <v-card-title>{{ item.name }}</v-card-title>

                            <v-card-subtitle>{{ item.description }}</v-card-subtitle>
                            </v-card-item>
                            <v-img height="200px" :src="item.image" cover ></v-img>

                            <v-card-text>{{ item.price }}</v-card-text>
                            <v-btn color="black" variant="tonal" @click="addToOrder(item)"> Order</v-btn>
                            
                        </v-card>
                        </v-col>
                </v-row>
            </v-container>
        </v-card>
    </v-container>
    <!-- My Orders -->

    <v-container>
        <v-card color="blue" >
            <v-card-title>
                <div class="text-h6">Current order: {{totalOrderAmount}}</div>
            </v-card-title>
        </v-card>
    </v-container>
    <v-container>
        <v-card class="mx-auto" elevation="24">
            <v-container>
                <v-row>
                    <v-col cols="12" md="4" v-for="item in orderItems" :key=item>
                        <v-card color="yellow">
                            <v-card-item>
                            <v-card-title>{{ item.name }}</v-card-title>

                            <v-card-subtitle>{{ item.description }}</v-card-subtitle>
                            </v-card-item>
                            <v-img height="200px" :src="item.image" cover ></v-img>

                            <v-card-text>{{ item.price }}</v-card-text>
                            <v-card-actions>
                                <v-btn color="black" variant="tonal" @click="removeFromOrder(item)"> Remove</v-btn>
                            </v-card-actions>
                        </v-card>
                        </v-col>
                </v-row>
            </v-container>
        </v-card>
    </v-container>
</template>

<script setup>
import { ref } from 'vue'
const menuItems = [
    {
        name: "Chips",
        price: 200,
        description: "Best chips in town",
        size: "Large",
        offers: "None",
        image: "/mitchell-luo-ChXHveqrb28-unsplash (1).jpg"
    },
    {
        name: "Sausage",
        price: 50,
        description: "Best sausages in town",
        size: "None",
        offers: "None",
        image: "/likemeat-cSxpCQrRlo8-unsplash.jpg"
    }
]

//manage the current state of the order
var orderItems = ref([])
var totalOrderAmount = ref(0)

function calculateTotalAmount(price){
    totalOrderAmount.value += price
}

function addToOrder(item){
    orderItems.value.push(item)
    calculateTotalAmount(item.price)
}

function removeFromOrder(item){
    orderItems.value.pop(item)
    totalOrderAmount.value -= item.price
}
</script>