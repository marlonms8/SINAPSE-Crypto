# Política de segurança

## Escopo

O SINAPSE Crypto existe para interoperabilidade com um formato criptográfico legado. Por esse motivo, utiliza parâmetros preservados deliberadamente, incluindo SHA-1, PBKDF2 com uma iteração e IV fixo.

Essas escolhas **não devem ser consideradas um padrão criptográfico moderno**.

## Dados

O aplicativo:

- não solicita permissão `INTERNET`;
- não envia textos ou chaves para servidores;
- não grava automaticamente o conteúdo criptografado, descriptografado ou a chave;
- processa as operações localmente no dispositivo.

## Relato de vulnerabilidades

Para problemas específicos do código do SINAPSE Crypto, utilize um issue no repositório e evite publicar textos, chaves ou outros dados reais usados na aplicação.
