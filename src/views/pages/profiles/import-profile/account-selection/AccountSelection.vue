<template>
  <div class="account-selection-container" @keyup.enter="submit">
    <div class="left-container">
      <div class="dialog-sub-tips">
        {{ $t('address_to_interact_with') }}
      </div>
      <div class="choose-hd-path radius scroll">
        <div class="address-list">
          <div class="table-title">
            <span class="address-id">{{ $t('id') }}</span>
            <span class="address-value">{{ $t('address') }}</span>
            <span class="address-balance">{{ $t('balance') }}</span>
          </div>
          <div>
            <div v-for="(a, index) in addressesList" :key="index" @click="onAddAddress(index)">
              <div v-if="!selectedAccounts.includes(index)" class="table-item pointer">
                <span class="address-id">{{ index + 1 }}</span>
                <span class="address-value">{{ formatters.miniAddress(a) }}</span>
                <span v-if="addressMosaicMap[a.plain()]" class="address-balance overflow_ellipsis">
                  <MosaicAmountDisplay :absolute-amount="addressMosaicMap[a.plain()]" />
                </span>
                <span v-else class="address-balance overflow_ellipsis">
                  N/A
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="right-container">
      <div class="right-container-title">
        {{ $t('select_accounts') }}
      </div>
      <div class="address-list-container radius scroll">
        <div class="address-list">
          <div class="table-title">
            <span class="address-id">{{ $t('id') }}</span>
            <span class="address-value">{{ $t('address') }}</span>
            <span class="address-balance overflow_ellipsis">{{ $t('balance') }}</span>
            <span class="remove-icon" />
          </div>
          <div class="radius">
            <div
              v-for="index in selectedAccounts"
              :key="index"
              class="table-item pointer"
              @click="onRemoveAddress(index)"
            >
              <span class="address-id"> {{ index + 1 }} </span>
              <span class="address-value">{{ formatters.miniAddress(addressesList[index]) }}</span>
              <span v-if="addressMosaicMap[addressesList[index].plain()]" class="address-balance overflow_ellipsis">
                <MosaicAmountDisplay :absolute-amount="addressMosaicMap[addressesList[index].plain()]" />
              </span>
              <span v-else class="address-balance overflow_ellipsis">
                N/A
              </span>
              <span class="remove-icon"><img src="@/views/resources/img/Invisible@2x.png" /></span>
            </div>
          </div>
        </div>
      </div>
      <div class="button-container flex-container">
        <button class="button-style info-button back-button" @click="previous">
          {{ $t('previous') }}
        </button>
        <button class="button-style validation-button" @click="submit">
          {{ $t('next') }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import AccountSelectionTs from './AccountSelectionTs'
export default class AccountSelection extends AccountSelectionTs {}
</script>
<style lang="less" scoped>
@import './AccountSelection.less';
</style>
