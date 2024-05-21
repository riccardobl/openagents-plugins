# OpenAgents - Plugins

A list of extism plugins for OpenAgents.



## Add a secret
1. Clone this repo and cd into it
2. Encrypt the secret
```bash
echo -n "mysecret" | openssl pkeyutl  -pkeyopt rsa_padding_mode:oaep -encrypt -pubin -inkey public.pem | base64 -w 0
```
3. Add the encrypted secret, prefixed with "enc:", to the `secrets.json` file under an object with the path to your plugin, or the sha256 hash of the path of your plugin, as the key
```json
{
    "link/to/your/plugin.wasm":{
        "mysecret": "enc:encrypted_secret"
    }
}
```
4. Use `%secret.mysecret%` (replace `mysecret` with your secret name) anywhere in your plugin template

Only our nodes will be able to decrypt the secret using our private key.