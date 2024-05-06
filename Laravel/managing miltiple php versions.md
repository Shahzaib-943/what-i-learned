
# Managing Multple PHP Versions
If you want to switch between different php version in ubuntu, we can do it with apt-ulternatives package.

Follow these steps to install the package and php versions.

Or follow this youtube tutorial 
[@Youtube Tutorial](https://www.youtube.com/watch?v=JujOdVADXgo)

## Steps :





Step-1 : Add this repo by following command.

```bash
sudo add-apt-repository ppa:ondrej/php
```


Step-2 : Install the package.

```bash
sudo apt-get install update-alternatives
```

We will install php8.2, for this tutorial.

Step-3 : Install the desired php version.
```bash
sudo apt update
sudo apt install php8.2
```

Step-4 : Manage the php versions by opening apt-alternatives prompt by given command, and by selecting thorugh index number.
```bash
sudo update-alternatives --config php
```

Step-5 : Install desried extensions for new php.
```bash
    sudo apt install php8.2-xml
    sudo apt install php8.2-dom
    sudo apt install php8.2-curl
    sudo apt install php8.2-mysql
    sudo apt install php8.2-sqlite3
```
Note, i installed php8.2 and installed extensions for it accordingly.


## Author

- [@Shahzaib](https://github.com/Shahzaib-943)

