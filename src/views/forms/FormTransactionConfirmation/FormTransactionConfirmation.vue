<template>
  <div class="form-transaction-confirmation">
    <FormWrapper :whitelisted="true">
      <form onsubmit="event.preventDefault()">
        <div class="transactionConfirmationBody">
          <div v-if="!!stagedTransactions" class="stepItem1">
            <div v-for="(transaction, index) in stagedTransactions" :key="index" class="info_container">
              <TransactionDetails :transaction="transaction" />
            </div>

            <HardwareConfirmationButton v-if="isUsingHardwareWallet" @success="onSigner" @error="onError" />
            <FormProfileUnlock
              v-else
              ref="unlockForm"
              :disable-submit="disableSubmit"
              @success="onAccountUnlocked"
              @error="onError"
            />
          </div>
        </div>
      </form>
    </FormWrapper>
  </div>
</template>

<script lang="ts">
import { FormTransactionConfirmationTs } from './FormTransactionConfirmationTs'
export default class FormTransactionConfirmation extends FormTransactionConfirmationTs {}
</script>

<style lang="less" scoped>
@import '../../resources/css/variables.less';
.float-right {
  float: right;
}

.clear-staged-transactions {
  font-size: @smallFont;
  cursor: pointer;
}
</style>
