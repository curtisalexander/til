# Custom Certificate in macOS 
In order to add a custom certificate into the system keychain in macOS, run the following (assuming your custom certificate is stored in the directory `~/.cert`).

```
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ~/.cert/ca-bundle.pem
```
