# HP LaserJet P1102 Drivers for macOS Tahoe 26.0.1

This guide provides a solution for installing HP LaserJet P1102 drivers on macOS Tahoe (26.0.1+). The official HP drivers refuse to install on newer macOS versions due to a version check in the installer. With a simple modification to bypass that check, you can get your printer working again on Tahoe.

This is a modified Version for MacOs Tahoe originally was made for macOS Sequoia check repo here: https://gist.github.com/pavelbinar/e14bb47f98768d83828bdee89a47490e#file-install-driver-sh 
made by : pavelbinar  https://gist.github.com/pavelbinar 

Anyways There you have it for Tahoe.

## Supported Printer Models

* HP LaserJet P1102
* HP LaserJet Pro P1102
* HP LaserJet Pro P1102w

## Manual Installation Steps

1. Download the official [HP Mac Printer Driver]([https://support.hp.com/us-en/drivers/hp-laserjet-pro-p1102-printer-series/model/4110303?sku=CE651A]) (e.g. from the HP driver .dmg).
2. Extract the `HewlettPackardPrinterDrivers.pkg` file from the `HewlettPackardPrinterDrivers.dmg` file.
3. From a terminal, go to the folder where you extracted the `.pkg` file and run:
   ```
   pkgutil --expand HewlettPackardPrinterDrivers.pkg drivers
   ```
4. Open the `drivers/Distribution` file in any text editor.
5. Change the fragment that says `system.version.ProductVersion, '15.0'` to `system.version.ProductVersion, '27.0'`.
6. Save the file.
7. From the terminal, run:
   ```
   pkgutil --flatten drivers HewlettPackardPrinterDrivers-tahoe.pkg
   ```
8. Optionally remove the `drivers` folder, and the original `.dmg` and `.pkg` files if you no longer need them.
9. The file `HewlettPackardPrinterDrivers-tahoe.pkg` is your new installer that works with macOS Tahoe 26.0.1.

## Automated Installation

For an automated installation, place the `install-driver.sh` script in the same directory as your `HewlettPackardPrinterDrivers.pkg` file (or in a folder where you have already expanded the package so that `Distribution` is in the current directory) and run:

```
chmod +x install-driver.sh
./install-driver.sh
```

The script will perform the version-check modification and create `HewlettPackardPrinterDrivers-tahoe.pkg`. You can then install the driver by double-clicking that package.

## Notes

* This solution should work with other HP printer models and installers that use the same kind of version check.
* It may work with future macOS releases by adjusting the version number in the Distribution file (use a value higher than your macOS version so the check does not block installation).
* No changes are made to the actual driver files, only to the installer’s version check.
* The installer’s `Distribution` file may also restrict to `x86_64`; on Apple Silicon you might need to adjust that if the package otherwise supports your Mac.

## Disclaimer

This is an unofficial workaround and is not officially supported by HP. Use at your own risk.

## Credits

This solution is based on the approach in [pavelbinar’s gist](https://gist.github.com/pavelbinar/e14bb47f98768d83828bdee89a47490e) for macOS Sequoia and the [blog post by Kartones](https://blog.kartones.net/post/macos-sequoia-hp-laserjet-p1102-drivers/).
