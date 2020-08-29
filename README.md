# Tagion AlphaOne Release

## What is Tagion Network

The Tagion network decentralizes trading and transferring between compatible cryptocurrencies and is operated by a democratic governance mechanism: the users of the network essentially own and control the network as it is open and technically accessible for everyone.

The network itself consists of a **gossip protocol,** which is used for data synchronization, the **hashgraph algorithm**, which provides consensus and ordering transactions, and the **sharding** **opportunity,** that lets transactions run in parallel and enhances the speed of the system.

## What is the Tagion AlphaOne release?

**AlphaOne** is Tagion's initial test network. It consists of a stable public network in which users can send payment requests and receive Tagions in order to test and enhance the system. Tagion **AlphaOne** is live for users, but it is a closed testnet; for access, please contact: [Roxana Nasoi](mailto:rn@i25s.com).

With **AlphaOne**, users can create wallets, request tagions from the administrator or an automated faucet, create and send payment requests, and transfer tagions between wallets either as a sender or receiver. 

# Tagion AlphaOne Manual

[TOC]

## Who is this manual for?

This manual is intended for Tagion **AlphaOne** network users who will send and receive Tagions over the network in order to build up both user experience and a stronger network. The manual focuses on the following:

- Creating the environment in which the wallet can be used;
- Accessing Tagion AlphaOne network via the wallet CLI;
- Creating and using the Tagion wallet to send and receive Tagions within the system.


## Preconditions and wallet download

Tagion **AlphaOne** runs on Linux, and there are means to run it on Windows, and macOS as well. The setup changes based on the OS being used, but `tagionwallet` CLI operation is the same.

### For **Linux** or **WSL** users:

If you have **Windows 10**, you can enable [WSL](https://www.windowscentral.com/install-windows-subsystem-linux-windows-10) and use wallet like you would on **Linux**.

1. [Download the wallet binary](https://github.com/tagion/alpha/releases/download/wallet_1.0/tagionwallet)
2. Check if it runs:

```
./tagionwallet --help
```

### For others - Docker:

If you don't have Linux or WSL, or just want to use Docker instead, we prepared an image for you.

If you don't have Docker, follow the [Getting Started With Docker](https://www.docker.com/get-started) guide first.

1. Make sure you have docker installed;
2. Run the following command:

```bash
docker run -it tagion/wallet bash
```

Or mount a volume to keep the tagionwallet files (change `Foo` to the folder to which you mount):

```bash
# On Windows:
docker run -it -v C:\Foo:/files tagion/tagionwallet bash

# On macOS or Linux
docker run -it -v ~/Foo:/files tagion/tagionwallet bash
```

This will run the image with the wallet already installed.

### Update your PATH

*You can skip this step, if you use our Docker image.*

To access `tagionwallet` from anywhere, the path to the binary should be known to your shell.

```bash
# Move the binary to some folder
mkdir ~/tagion/bin
mv ./tagionwave ~/tagion/bin/

# Will update PATH for this shell session only:
export PATH:$PATH:~/tagion/bin/

# Now you can run tagionwave from anywhere
tagionwave --help
```

## About Tagion Wallet CLI

CLI sends requests directly to running nodes, so for each command that talks to the node, you have to specify the IP address of that node:

```bash
# Flag to specify the Node IP to send request to:
-u [ip address]

# Example that updates the local bills:
tagionwallet --update -u 127.0.01
```

Basic commands for the `tagionwallet`:

```bash
# Enter GUI mode for creating 
# wallet or generating invoices:
tagionwallet -g 

# Update the local bills.hibon:
tagionwallet --update -u 3.249.14.175

# Print amount based on your local bills.hibon:
tagionwallet --amount

# Shortcut for updating and printing:
tagionwallet --update --amount -u 3.249.14.175

# Fulfil a payment request
tagionwallet --pay ./invoice.hibon -x 1111 -u 3.249.14.175 --send
```

## AlphaOne Node IP Addresses

When sending requests via the CLI, you can use any running node IP. Here is a list of the first 11 nodes:

```
3.250.150.166
34.241.136.45
34.242.210.219
34.242.120.199
63.32.90.80
3.249.14.175
54.74.68.133
34.245.73.196
3.250.143.172
34.251.132.77
52.31.179.105
```

## Create two wallets

Tagion does not have an accounting system, like most blockchains do. Instead, we store the bills in the database. The wallet software manages the keys for those bills. You can 'spend' the bills using the Tagion compatible wallet, in our case - Wallet CLI.

To send Tagions from one wallet to another, the sender must know the public key of the receiver. Currently, we use a primitive system of **payment requests** (previously called *invoices*) for this. The receiver must generate the payment request, and this will be fulfilled by the sender.

**Let's create some Wallets!**
Create two folders, one for each wallet. Let's name them `w1` and `w2` accordingly.

``` bash
mkdir w1 w2
```

Now from each folder, enter the GUI mode and create the wallet for each folder:
```bash
cd w1
tagionwallet -g # Enter the GUI mode
# Press 'c' to enter the creation menu
# Use arrows and 'Enter' to navigate through recovery questions
# Answer at least 3 questions
# Press 'c' again to confirm
# Enter a 4-digit pin code. This will be used for payments later
# Press 'Enter', and hooray, you are done
# Quit the GUI mode by pressing `q` until you are out

cd ../w2
# Repeat the process
```

## Request Tagions

You need some Tagions to pay from one wallet to another. You have two options here - request some test Tagions from us in the forum, or try our automated faucet.

You need to generate a payment request and send the generated file `invoice.hibon` to us in the forum.

```bash
./tagionwallet -g # Enter GUI mode
# Enter Pincode
# Press 'a' to enter account
# Press 'i' to enter invoice mode
# Type the invoice label, press enter and fill the sum of Tagions to generate
# Quit the GUI mode by pressing `q` until you are out

# ./invoice.hibon should appear
```

### How to request test tagions in the forum

Send us the generated `./invoice.hibon` in the forum [WILL PASTE THE LINK] and we will fulfil it within a day.

### How to request test tagions via the faucet

Send the `invoice.hibon` to our API:

```bash
curl -F paymentRequest=@invoice.hibon api.monitor.tagion.org/faucet/print
```

### Check balance

In 5 to 10 seconds, check the balance

```bash
tagionwallet --update --amount -u 3.249.14.175
```

You should see that your balance has changed;

## Transfer test Tagions between wallets

Now you have Tagions in one of your wallets, you can send them to another wallet. In this guide we will show you how to send to your second wallet, that you create previously.

```bash
# Go to your empty wallet's folder
cd w2

# Generate a payment request, as you did in the previous step
tagionwallet -g # Enter GUI to generate payment request (invoice)

# Go to your wallet with Tagions
cd ../w1
tagionwallet --pay ../w2/invoice.hibon -x [your pin-code] -u 3.249.14.175 --send

# Check balance in 10 seconds
tagionwallet --update --amount -u 3.249.14.175

# Once the balance is updated, you can make sure it is also
# updated in the second wallet:
cd ../w2
tagionwallet --update --amount -u 3.249.14.175
```


## Conclusion

In this manual you used the Tagion Wallet CLI and public AlphaOne network to send and receive testnet Tagions. Behind the scenes, nodes reach a consensus regarding the order of transactions using the Hashgraph algorithm, and stored and synced data using the DART database. The network is still in the early stages of development, but you witnessed the basic protocols running smoothly.

## Troubleshooting

If you have any problems, please let us know by opening an issue [LINK TO OPEN AN ISSUE].

If you questions or need some help, ask us in the Telegram chat [LINK TO TELEGRAM CHAT].

<!-- ### Known problems -->
