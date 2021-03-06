# OlympicCoin Masternode Startup Guide with script

## Installing a OlympicCoin masternode on a Linux server running Ubuntu 16.04:

1. Connect to your VPS via command line and enter the following code:

```
wget -q https://olympcoin.io/assets/olympic_install.sh && chmod +x olympic_install.sh && ./olympic_install.sh
```

2. Wait for the installation to finish and let the script generate a **private key (genkey)** for you.

3. Create a new text file in your editor. Chose an alias for your masternode (MN1 for example) and copy the **ip:port** and **genkey** from the installation outputs and paste it after the alias so it looks like this:

```
MN1 ip:port genkey
```

4. Wait until the blockchain is **fully synced**. You can check the block count with:

```
olympic-cli getblockcount
```

or

```
olympic-cli getinfo
```

and compare it to the current block number on https://explorer.olympcoin.io/ or in your wallet under **Help > Debug window > Information**

***

## Preparing and setting up the OlympicCoin desktop wallet

Now that your coin daemon on VPS is up and running, it is time to configure the desktop wallet. The following steps will show you how to do it:

1. Open up the OlympicCoin desktop wallet.

2. Go to **"Settings > Options > Display"** (**"Preferences > Display"** for MAC) and make a **checkmark** at **"Display coin control features (experts only!)"**.

3. Now we need to edit the wallet configuration file (**olympic.conf**) which you will find here:

**Windows**

```
C:\Users\Username\AppData\Roaming\OlympicCoin
```

Tip: It is easier to locate the folder when you have the displaying of hidden files activated (search in google for: show hidden files in windows).

**MAC**

```
/Users/Username/Library/Application Support/OlympicCoin
```

Tip: It is easier to locate the folder when you have the displaying of hidden files activated. To show hidden files on MAC OS X open up the terminal and type:

```
defaults write com.apple.finder AppleShowAllFiles YES
killall Finder
```

4. Right click on the **olympic.conf** file and open it up in a text editor. Then paste the following line at the end of the file:

```
mnconflock=1
```

Save and close the file.

5. Now open up your wallet again, go to the Receive tab and create a New Address: **MN1**. Right click on the newly created address and select "Copy Address".

6. Switch to the Send tab and send exactly choosed amount: **1M OLMP**, **2M OLMP** or **3M OLMP** to this address.

7. Go to the Transactions tab and wait for the first confirmation.

8. Open up **Help > Debug window > Console** and type:

```
masternode outputs
```

9. Copy the **txid** (first part) and the **index** (second part: 0 or 1) of the output and paste it in the text file where you inserted your ip:port and private key before so it looks like this:

```
MN1 ip:port genkey txid index
```

Mark the line and copy it.

10. Now go to the folder where your olympic.conf is located at, open up the **masternode.conf** file with your editor and paste the masternode configuration line at the end of it *(Note: If the file doesn't exist already, create it with your text editor and make sure you save it with the **.conf** extension)*.

Save and close the file.

11. Restart your wallet.

12. Once the transaction has **15 confirmations** switch to the **Send tab** and click on **"Inputs ..."** under **Coin Control Features**. Switch to **"List mode"**, right click your masternode transaction and select **"Unlock unspent"**.

13. Now switch to the **Masternodes tab**, click **Update**, select the masternode you want to start and press **"Start"**. You will now get a message that the masternode has been successfully started. Click on **"Update"** again to see that your **Masternode is Running**.

14. Go to the **Coin Control Features** again, switch to **"List mode"** and set **"Lock unspent"** on your masternode transaction again **IF IT IS NOT LOCKED**.

15. To double check that your masternode is properly running, switch back to your VPS and type:

```
olympic-cli masternode status
```

You should receive **"status: Masternode is running remotely"**.


### Congratulations, you have just set up your first OlympicCoin masternode!


## IMPORTANT: Always make sure your masternode transactions are locked before you send coins, else it might destroy the transaction and you have to set it up again.

## If you want to set up multiple masternodes:

Create a new address for the Masternode (e.g. MN2). Follow the steps **6 - 9**. Then go to your **Coin Control Features** and **lock** the newly created masternode transaction. Repeat those steps for each additional masternode.
 
## VPS commands:
```
olympic-cli getblockcount
olympic-cli getinfo
olympic-cli masternode status
```
Also, if you want to check/start/stop **OlympicCoin**, run one of the following commands as **root**:

**Ubuntu 16.04**:
```
systemctl status OlympicCoin.service #To check the service is running.
systemctl start OlympicCoin.service #To start the service.
systemctl stop OlympicCoin.service #To stop the service.
systemctl is-enabled OlympicCoin.service #To check whetether the service is enabled on boot or not.
```
