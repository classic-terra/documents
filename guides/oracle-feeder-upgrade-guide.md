# Oracle-Feeder Upgrade Guidelines - 24/02/2023

## Introduction
Oracle Feeder is the L1 platform `side-car capability` responsible for maintaining a bridge between the Terra Classic blockchain and external data sources providing `data points` to support the operation of on-chain modules. This particular `side-car capability` consists of two L2 NodeJS applications that collectively maintain a [price-server](https://github.com/classic-terra/oracle-feeder/tree/main/price-server) responsible for fetching `data points` from various external APIs & a [feeder](https://github.com/classic-terra/oracle-feeder/tree/main/feeder) that converts `data points` into a format that can be submitted to on-chain modules via a vote from each individual validator, thus ensuring consensus on the values recorded on-chain.

## Upgrade steps
In order to upgrade the Oracle Feeder you need to complete the below steps.

### Step #1 - Delete existing Oracle Feeder installation
Remove your existing Oracle Feeder installation.

***Note*** <br/>
Do not delete your installation if you do  not have access to your password or mnenomic. In case either of these cases hold true please create a new discussion item @ https://github.com/classic-terra/core/discussions/categories/support 

### Step #2 - Clone Oracle Feeder repository
git clone https://github.com/classic-terra/oracle-feeder.git
git checkout [COMMIT_ID]

### Step #3 - Setup Feeder application
https://github.com/classic-terra/oracle-feeder/tree/[COMMIT_ID]/feeder#instructions

### Step #4 - Setup Price-Server application
https://github.com/classic-terra/oracle-feeder/tree/[COMMIT_ID]/price-server#instructions

