# Some linux config things

## Uninstall node

to uninstall node , it can be done with the following :

```bash
sudo apt-get remove nodejs
```

then you'd have to remove the configurations.

```bash
sudo apt-get purge nodejs
```

then the following will remove some remaining files

```bash
sudo apt-get autoremove
```

## To Install node

- So apparently, we need to install the primer.. its called the PPA.Its installed in 2 commands.
  - the first command:

```bash
    nod
```

  - The second command:  

    ```bash
         curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
    ```

## Sources

Where I found install and uninstall files

https://www.digitalocean.com/community/tutorials/install-uninstall-nodejs-ubuntu