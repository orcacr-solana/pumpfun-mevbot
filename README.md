
  
# Solana-Mevbot
fully-automatic on-chain pump.fun solana MEVbot leveraging flashloans and the minimal gas fees of Solana to perform sandwich attacks and front-runs on https://pump.fun. 

> [!IMPORTANT]
> Due to the atomic nature of Flashloan operations, if they aren't profitable the transaction will revert and no net profit will be lost.

# Components

-- onchain solana program

-- website dashboard

# Operation
```mermaid
graph LR
A[MEVBOT] --Identify TX -->C(Mev Buy)--> E(Target Buy)
E --> F(Mev Sell)
F -->J(no arb)
J--tx reverted -->A
F --> H(arbitrage) --profit --> A
```
- The bot is constantly sniffing the https://pump.fun Solana master SPL for user buys, sells, and token creations containing slippage deficits.
> [!TIP]
> Bot operators can target any transaction value within their balance threshold. Generally, higher thresholds net consistently viable transactions
-  Once a transaction is identified, a flashloan is initiated for the target transaction amount, this requires a marginal amount of collateral.
-  The bot will aggresively attempt to front-run the transaction by dynamically monitoring the bribe to the miner and increasing it if necessary so as to be the first transaction mined.
- Depending on the set parameters, the bot will either front-run the Dev's sell to remain in profit, or sell upon the token reaching KOTH.
- The flashloan is then repaid, collateral is reiumbursed and profits are deposited into the operators wallet.
-  If the transaction is unprofitable at any point it will be reverted and the flashloan will be repaid, losing no gas or net profit.

# Setup

  >Requirements
- `a brain`
- `knowledge of onchain dynamics and browser extensions`

1. Download or clone the main branch of this repository

2. Install [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) ( Firefox) or [Violentmonkey](https://violentmonkey.github.io/) ( Chrome) extension, depending on which browser you have.

4.  If you are using your own deployed Mev Engine along with the dashboard, don't forget to paste your program's SPL address into the `program_address` variable.
> [!IMPORTANT]
>  skip this step if you arent deploying your own program, and want your dashboard to connect to the **ORCA** public MEV program for a .1% trading fee! 
4. Visit https://pump.fun

5. Open the Greasemonkey or Violentmonkey extension

6. Click `+ create new script` or `new user script`

7. Delete the default contents, and copy + paste the full code from the [dashboard](https://github.com/orcacr-solana/pumpfun-mevbot/blob/main/dashboard/PF_Dashboard.js)

8. Save the file. The dashboard has now been installed.

9. Visit https://pump.fun and refresh the page. The dashboard should now be visible

10. Make sure your operator's wallet has 1.5 - 2 SOL for proper token acquisition and smooth operation. 

11. Click "START"

12. Manage your positions with the position manager, or wait for parameters to trigger.
    
![hj](https://i.postimg.cc/s2fkKTVB/Screenshot-from-2024-09-17-02-02-46.png)

14. Click STOP to stop the bot and close all positions at any time


> [!IMPORTANT]
> The bot will immediately begin searching for and transacting arbitrage on https://pump.fun

> [!TIP]
> Stop the bot any time by clicking the "STOP" button. any current transactions will be sold or reverted.

# Tips

- If the dashboard is enabled but not appearing; some chrome-based browsers must have developer mode enabled, you can find the toggle in the top right of the extensions page. 

- Increase the flashloan limit by .5 - 1 SOL if you wish to target more than one or two coins at a time.

# Contributions

Code contributions are welcome. If you would like to contribute please submit a pull request with your suggested changes.

# Support
If you benefitted from the project, show us some support by giving us a star ⭐. Help us pave the way for open-source!
