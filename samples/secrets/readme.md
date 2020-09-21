## Secrets

#### Create a new secret (Basic string data)
[Secret sample] (secret1.yml)

#### Convert from string to base64 before storing the credentials as plain text
```shell script
echo "samson" | base64
echo c2Ftc29uCg== | base64 --decode
```

#### Create pod that access the secrets
