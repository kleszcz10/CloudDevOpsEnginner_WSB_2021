## LAB 09

### Utworzenie resource group

`az group create -n wsb-kv-1 -l westeurope`

### Utworzenie Key Vault

`az keyvault create -n pw26799-kv-1 -l westeurope -g wsb-kv-1`

### Utworzenie sekretu

`az keyvault secret set -n first-secret-in-my-kv --value ThisIsSecretValue --description ‘Moje pierwsze haslo w kv’ --vault-name pw26799-kv-1`

### Polecenie PS do wyświetlenia wartości przechowywanej w Key Vault
`Write-Host $(first-secret-in-my-kv)`

![Result](screen.png)

### Przygotowanie pipeline w formie yaml

```yaml
trigger:
- master

pool:
  vmImage: ubuntu-latest

variables:
- group: "pw26799-kv-2"

steps:

- script: |
    echo "secret-in-my-kv :" $(secret-in-my-kv)
  displayName: 'Value of secret-in-my-kv'
  ```

![Result](screen2.png)