# Como Armazenar e Usar Connection Strings do Azure Key Vault em Container Apps

## 1. Criar um Azure Key Vault
Se você ainda não tiver um Key Vault, crie um através do Azure Portal, CLI ou ARM Template.

## 2. Adicionar a Connection String ao Key Vault
1. No Azure Portal, vá para o seu Key Vault.
2. Selecione "Secrets" no menu à esquerda.
3. Clique em "Generate/Import" e adicione sua connection string como um novo segredo.

## 3. Configurar a Identidade Gerenciada (Managed Identity) para o Container Apps
1. Navegue até o seu Container App no Azure Portal.
2. No menu à esquerda, selecione "Identidade".
3. Habilite a identidade gerenciada (System assigned ou User assigned).
4. Anote o ID do recurso da identidade gerenciada, pois será necessário para conceder permissões no Key Vault.

## 4. Conceder Permissões ao Key Vault
1. Retorne ao seu Key Vault no Azure Portal.
2. Selecione "Access policies" no menu à esquerda.
3. Clique em "Add Access Policy".
4. Selecione as permissões "Get" e "List" para "Secrets".
5. Em "Principal", adicione a identidade gerenciada que você configurou no seu Container App.
6. Salve as alterações.

## 5. Configurar o Container App para Usar o Key Vault
1. No Azure Portal, vá até o seu Container App.
2. No menu à esquerda, selecione "Configurações".
3. Adicione uma nova variável de ambiente.
4. Defina o nome da variável de ambiente.
5. No valor, use o formato:
   ```plaintext
   @Microsoft.KeyVault(SecretUri=https://<nome-do-seu-key-vault>.vault.azure.net/secrets/<nome-do-segredo>)
