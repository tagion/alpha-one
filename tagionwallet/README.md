# Tagion Wallet CLI

Tagion Wallet CLI keeps track of your tagion bills locally and allows you to send and receive tagions, communicating directly with Tagion Nodes.

> [Download Latest Release of Tagion Wallet CLI](https://github.com/tagion/alpha_one/releases)

## Usage

```bash
./tagionwallet [<option>...]      

<option>:
          --version display the version
-w         --wallet Walletfile : default tagionwallet.hibon
-c        --invoice Invoicefile : default invoice.hibon
   --create-invoice Create invoice by format LABEL:PRICE. Example: Foreign_invoice:1000
-t       --contract Contractfile : default contract.hibon
-s           --send Send contract to the network
           --amount Display the wallet amount
-I            --pay Invoice to be payed : default
-U         --update Update your wallet
-m           --item Invoice item select from the invoice file
-x            --pin Pincode
-p           --port Tagion network port : default 10800
-u            --url Tagion url : default localhost
-g         --visual Visual user interface
-h           --help This help information.
```

## Visual UI

Tagion Wallet CLI has the interactive visual UI mode, that allows you to **create wallet** and generate **payment requests**.

```bash
tagionwallet -g # Enters the visual UI
```

If you open visual UI in a folder **without** `tagionwallet.hibon` file, you will be suggested to **create wallet** (press `c`).


If you open visual UI in a folder **with** `tagionwallet.hibon` file, you will be suggested to enter your Pincode and create an invoice (press `a`, then `i`).

## Questions

For questions and support please use the [official forum](https://forum.tagion.org/c/development/6) or [Telegram chat](https://t.me/tagionChat). The issue list of this repo is exclusively for bug reports and feature requests.

## Issues

Please use GitHub to [report a bug](https://github.com/tagion/alpha_one/issues/new?assignees=cbleser%2C+alexSushko&labels=bug&template=bug_report.md&title=) or [request a feature](https://github.com/tagion/alpha_one/issues/new?assignees=alexSushko%2C+cbleser&labels=enhancement&template=feature_request.md&title=).