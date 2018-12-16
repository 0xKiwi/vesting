# Vesting contract

## Configuration

In order to run tests you must configure the `config.js` to what parameters are needed, as the tests rely on these.

| Config            | Explanation                                               | Default                                        | Requirements                                   |
| ----------------- | --------------------------------------------------------- | ---------------------------------------------- | ---------------------------------------------- |
| MONTHS_TO_CLIFF   | The amount of months the cliff should last                | 12                                             | Must be even                                   |
| MONTHS_TO_RELEASE | The amount of months the releasable duration should last  | 24                                             | Must be even                                   |
| VESTED_TOKENS     | The total amount of tokens to be vested                   | 1200                                           | Must be cleanly divisible by MONTHS_TO_RELEASE |
| FIRST_PHASE       | The amount of months to be tested one-by-one              | MONTHS_TO_RELEASE / 2                          | Must be a whole number                         |
| SECOND_PHASE      | The amount of months to be skipped over after FIRST_PHASE | 2                                              | Must be a whole number                         |
| THIRD_PHASE       | The amount of months to do in one chunk at the end        | MONTHS_TO_RELEASE - FIRST_PHASE - SECOND_PHASE | Must be a whole number                         |

After setting up `config.js`, run `yarn test` to begin the tests.

## Deploying

To deploy the contract, you must first set the parameters for the function:

| Parameter       | Explanation                                                              | Default             | Requirements                           |
| --------------- | ------------------------------------------------------------------------ | ------------------- | -------------------------------------- |
| beneficiary     | The address of the person supposed to receive the tokens after vesting.  | none                | none                                   |
| token           | The address of the token being vested.                                   | none                | Must be a token address                |
| start           | The unix timestamp (seconds) of when the vesting should start.           | Date.now() / 1000   | Must be in seconds                     |
| cliffDuration   | The duration of the cliff in seconds.                                    | CLIFF_DURATION      | Must be divisible by SECONDS_PER_MONTH |
| vestingDuration | The total duration of the vest in seconds (including cliff).             | TOTAL_VEST_DURATION | Must be divisible by SECONDS_PER_MONTH |
| revokable       | If the owner of the contract should be able to revoke unreleased tokens. | false               |                                        |
| totalTokens     | The total amount of tokens being vested.                                 | VESTED_TOKENS       | Must be divisible by MONTHS_TO_RELEASE |

### Deploying to the network

Set the private key and proper RPC url in the web3 provider

Once these are set, run `yarn deploy.js`
