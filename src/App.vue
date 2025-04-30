<template>
  <v-app>
    <v-layout>
      <v-app-bar class="text-center">
        <v-app-bar-title class="text-h5 font-weight-bold">Nova ordem de serviço</v-app-bar-title>


        <template v-slot:append>
          <v-btn
            icon="mdi-bug"
            :color="debug ? 'pink' : 'black'"
            @click="debug = !debug"
          />
        </template>
      </v-app-bar>

      <v-main class="mt-6">
        <v-container>
          <v-row>
            <v-col>
              <h3>Organizações Tabajara</h3>
              Avenida Dom Eugênio Sales, 96 - Boca do Rio <br>
              Salvador - Bahia 41715-030 <br>
              Tel: 71 9999-9999 <br>
              E-mail: contato@tabajara.com.br
            </v-col>

            <v-col>
              <OSDetails/>
            </v-col>
          </v-row>

          <div class="mt-8">
            <OSClient/>
          </div>

          <div class="mt-8">
            <OSServices/>
          </div>

          <div class="mt-6">
            <v-row>
              <v-col>
                <v-textarea
                  v-model="description"
                  label="Descrição da ordem de serviço"
                  hide-details
                  variant="outlined"
                />
              </v-col>

              <v-col>
                <OSTotal/>
              </v-col>
            </v-row>
          </div>

          <div class="mt-8 text-right">
            <v-btn variant="text">Cancelar</v-btn>
            <v-btn color="primary" @click="onSubmit">Enviar</v-btn>
          </div>

          <template v-if="debug">
            <hr class="my-6">
            <b>Detalhes:</b> {{orderDetails}} <br>
            <b>Cliente:</b> {{client}} <br>
            <b>Servicos:</b> {{services}} <br>
            <b>Descrição:</b> {{description}} <br>
            <b>Tipo de Desconto:</b> {{discountType}} <br>
            <b>Valor do Desconto:</b> {{discountValue}} <br>
            <b>Subtotal:</b> {{subtotal}} <br>
            <b>Total:</b> {{total}} <br>
          </template>
        </v-container>
      </v-main>
    </v-layout>
  </v-app>
</template>

<script setup>
import {useServiceOrderStore} from './store/serviceOrder.js';
import {ref} from 'vue';
import OSDetails from './components/OSDetails.vue';
import OSClient from './components/OSClient.vue';
import OSServices from './components/OSServices.vue';
import OSTotal from './components/OSTotal.vue';
import {storeToRefs} from 'pinia';

const serviceOrderStore = useServiceOrderStore()
const {
  orderDetails,
  client,
  services,
  description,
  discountType,
  discountValue,
  subtotal,
  total,
} = storeToRefs(serviceOrderStore)
const debug = ref(false)

function onSubmit() {
  if (debug.value) {
    console.log({
      'Detalhes': orderDetails.value,
      'Cliente': client.value,
      'Servicos': services.value,
      'Descrição': description.value,
      'Tipo de Desconto': discountType.value,
      'Valor do Desconto': discountValue.value,
      'Subtotal': subtotal.value,
      'Total': total.value,
    })
  }
}
</script>
