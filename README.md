# Skywallet-Manager
This is a program that helps synchronize skywallets automatically and also adds security and performance.  

## Purpose: 

To keep a merchan't skywallet syncronized, small enough to work with (performance) and reduce the risk of theft.

## How it works: 
NOTE: This program will probably call raidaGo to actaully execute the transfers. 
1. When the program starts, it will look at all the wallets in the Receive and Storage folders. It will then ask the user to give a password if it finds ".txt" files. If it finds png or stack files, it will not ask the user for a password. If the passwords are not written on the hard drive. Hackers would need to steal them out of RAM and that would be difficult. 
2. After the passwords are given (if .txt), the program detects on the password to see if it is good. If bad, the user is told it is bad. 
3. Then the program will tell the user: "Syncronizing Wallets." It will get the balance of each skywallet and see if sync transfer needs to be called. It does this one skywallet at a time. When the balance has been received, it is put in the file name of the Skywallet name. 
4. Each Skywallet is given a file whose name is the same as the skywallet. The file is empty but the balance in the skywallet is kept as part of the file name. 
5. The Skywallet manager can now look at the file names to determine if the Receive Skywallet is too full or too empty. If it is too full it will pull coins out starting with the smalles denominations but leaving enough small ones so that change is not neccessary. So it will probably mainly pull out 100CC notes but leave 250s. 
6. If the Receive has too few coins, this program will move coins from a Store to the Receive Folder 
7. The program will transfer coins from the Receiver to the Storage account with the least amount of coins in it. This way, the amount of each Storage wallet will fill up slowly. 
8. If the storages becomes full and local wallet overflow = true in the confi file, coins will be stored on the local default wallet. Otherwise, a warning email will be sent out and the Storage Skywallets will continue to be filled past their max amount. NOTE: The local wallet overflow can be phase 2. 
12. This cycle is repeated according to the minutes= setting in the config file.  

## Requirments
Should be able to run on Linux Servers.

Folder Structure:
```bash
|-CloudCoin Wallet
|-- skywallet_manager.exe
|-- skyallet_manager_config.txt
|-- ID
    |-- Receive
	      |-- cc00.Folgory.com.349822.txt
	      |-- config.txt
    |-- Storage
        |-- cc01.Folgory.com.5000000.txt
        |-- cc02.Folgory.com.5000000.txt
        |-- cc03.Folgory.com.5000000.txt
        |-- cc04.Folgory.com.5000000.txt
        |-- cc05.Folgory.com.5000000.txt
        |-- cc06.Folgory.com.3400500.txt
|-- Accounts
     |-- DefaultWallet
	       |-- Bank
	       |-- Fracked
	       |-- Lost
	       |-- Etc...
|-- Logs
    |-- skywallet_manager.log
```
# Sample Config File:
```toml
# This is a TOML document.
[sync]
  minutes = 20
  [receive]
  max_notes = 10000
  max_coins = 3000000
  min_coins = 300000
  min_hours = 3 //How long coins must be in the Skywallet before they are removed (To make sure coins are not removed before counted)
  [storage]
  max_notes = 50000
  warn_email = ["Sean@Worthington.net","bill@folgory.com"]
  [local_wallet]
  overflow = true
  ```
