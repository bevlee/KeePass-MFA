## Multi-factor Authentication on KeePass using a secret sharing scheme
This program integrates Shamir Secret Sharing with KeePass.  
Shamir Secret Sharing is an algorithm that splits a secret up into n shares with a threshold of k. Only when k shares are combined, can the original secret be restored.  
Shamir Secret Sharing is used on KeePass databases in this project. A user can choose n and k to split the database into shares on different devices.  
When bringing together at least k of them, the database can be reconstructed. 

This project also implements a versioning scheme which tracks previous versions of shares. By doing this, different versions of databases can be represented by different combinations of shares.  
Users can therefore update the database using Shamir Secret Sharing without requiring all devices/shares to be present.  

Currently, users can only split the database into up to 5 shares/devices.

## System Requirements
This is based on KeePass version 2.41

This program uses the version 4.6 of the .NET framework.  
All Windows operating systems later than Windows XP will have this installed by default.  
If an older version of Windows is used, .NET is required to run KeePass.  
KeePass is designed to be a portable password manager that can run simply from devices such as a USB stick.

KeePass is also able to run on Linux and MacOS systems using Mono to enable the .NET functionality.  
Although these platforms are supported for the official KeePass project, this was not tested in this project so it may not work smoothly.

## How to Use: 
Run KeePass.exe in KeePass/Build/KeePass/Release/

This program does not modify existing features of KeePass, so you can refer to https://keepass.info/index.html for general KeePass information.

To use the additional secret sharing functionality, there are additional options available in the file menu:

### ShamirOpen  
Allows the user to select a number of shares to use to reconstruct a KeePass Database (.kdbx) file. The user needs to specify the Threshold or the minimum number of shares required to reconstruct the secret.  
It will then prompt the user for the password to the database if it is successfuly constructed.  
This operation will attempt to give the user the most up-to-date database by opening all possible databases given the shares, and merge them.

### ShamirQuickSave 
- Requires a database to be open.  
- Requires the database to have been opened using shares with the devices that have the shares to be present.

Note: This will not work if a device with a share used to open the database is disconnected prior to running ShamirQuickSave.  

Saves the database as shares to the locations used to open the current database.  
This keeps a history of the previous shares for each location specified.  
If there are different versions of databases on different sets of shares, the program will attempt to merge all databases that can be reconstructed to give the most updated password entries possible.  


### ShamirSynchronize 
- Requires a database to be open.  

Similarly to ShamirSave,
saves the database to n number of locations as shares, requiring k shares to reconstruct as specified by the user.  
The difference here is it overwrites the history

## Notes
The program only accepts a (5. 3) threshold scheme right now.  
If the database that you are trying to split is large, then it will take some time to split and reconstruct the database.  
I have provided a small example KeePass database (database.kdbx) in the root folder. This will ensure that the operations all work quickly.  
The password is: "password"  
Please do not change the master password unless you have all shares/devices present.  
If you change the master password without them present, the merging function will not work between multiple database versions.

