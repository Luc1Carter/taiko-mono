<script lang="ts">
  import { t } from 'svelte-i18n';

  import AmountInput from '$components/AmountInput';
  import Button from '$components/Button/Button.svelte';
  import { Card } from '$components/Card';
  import { ChainSelector } from '$components/ChainSelector';
  import Icon from '$components/Icon/Icon.svelte';
  import { ProcessingFee } from '$components/ProcessingFee';
  import { RecipientInput } from '$components/RecipientInput';
  import { TokenDropdown } from '$components/TokenDropdown';
  import { type Token, tokens } from '$libs/token';
  import { destChain, srcChain } from '$stores/network';

  let selectedToken: Token;
</script>

<Card class="md:w-[524px]" title={$t('bridge.title')} text={$t('bridge.subtitle')}>
  <div class="space-y-[35px]">
    <div class="space-y-4">
      <div class="space-y-2">
        <ChainSelector label={$t('chain.from')} value={$srcChain} />
        <TokenDropdown {tokens} bind:value={selectedToken} />
      </div>

      <AmountInput token={selectedToken} />

      <div class="f-justify-center">
        <button class="f-center rounded-full bg-secondary-icon w-[30px] h-[30px]">
          <Icon type="up-down" />
        </button>
      </div>

      <div class="space-y-2">
        <ChainSelector label={$t('chain.to')} value={$destChain} />
        <RecipientInput />
      </div>
    </div>

    <ProcessingFee />

    <div class="h-sep" />

    <Button type="primary" class="px-[28px] py-[14px]">
      <span class="body-bold">{$t('bridge.button.bridge')}</span>
    </Button>
  </div>
</Card>
