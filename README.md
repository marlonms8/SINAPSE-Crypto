# SINAPSE Crypto

Aplicativo Android offline para **criptografar e descriptografar textos em AES/CBC**, com interoperabilidade byte a byte com o padrão legado **Collura Decrypter v1.0**.

## Recursos

- **Editor em tela cheia** para o texto de entrada e para o resultado, ideal para mensagens longas.

- Kotlin + Android SDK nativo
- AES-128-CBC / PKCS5Padding
- Compatibilidade com Collura Decrypter v1.0
- Funciona 100% offline
- Não solicita permissão de Internet
- Nenhum texto ou chave é persistido pelo aplicativo
- Tema claro/escuro seguindo o sistema
- Mostrar/ocultar chave
- Criptografar, descriptografar, copiar e limpar
- Ícone próprio do SINAPSE Crypto
- Min SDK 23 / Target SDK 35

## Compatibilidade

O modo criptográfico reproduz o comportamento legado necessário para interoperabilidade:

- Cifra: `AES/CBC/PKCS5Padding`
- Chave: AES-128
- IV: 16 bytes `0x00`
- Senha: UTF-8 → SHA-1
- Digest SHA-1: Base64 Android `NO_PADDING`, preservando o LF final usado pelo comportamento legado
- KDF: `PBKDF2WithHmacSHA1`
- Salt: `Salt`
- Iterações: `1`
- Chave derivada: 128 bits
- Resultado: Base64

### Vetores de compatibilidade validados

| Texto | Chave | Resultado esperado |
|---|---|---|
| `teste` | `123456` | `aMS10Jp7EWXiOT+FcQxGRw==` |
| `teste1` | `123456` | `vgZ2fqx1dsnYp7/+rQdJ5w==` |
| `teste` | `654321` | `PHnyQlWpUWo0T4ktBAQqEg==` |

Esses vetores foram usados como teste de aceitação durante a implementação.

## Estrutura

```text
SINAPSE_Crypto/
├── app/
│   ├── build.gradle.kts
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/sinapse/crypto/
│       │   ├── ColluraCrypto.kt
│       │   └── MainActivity.kt
│       └── res/
├── docs/
│   └── COMPATIBILITY.md
├── .github/
│   └── ISSUE_TEMPLATE/
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── LICENSE
├── THIRD_PARTY_NOTICES.md
├── CHANGELOG.md
├── SECURITY.md
└── README.md
```

## Abrir no Android Studio

1. Clone ou baixe o repositório.
2. Abra a pasta raiz `SINAPSE_Crypto` no Android Studio.
3. Selecione **JDK 17** para o Gradle.
4. Instale o **Android SDK 35**, se necessário.
5. Aguarde o Gradle Sync.
6. Execute em um aparelho/emulador ou use **Build → Build APK(s)**.

O APK de debug normalmente será criado em:

```text
app/build/outputs/apk/debug/app-debug.apk
```



## Segurança e escopo

O aplicativo preserva deliberadamente um esquema criptográfico legado para interoperabilidade. Os parâmetros não representam uma recomendação de desenho criptográfico moderno e não devem ser usados como referência para proteção de material de alta sensibilidade.

A aplicação não possui permissão `INTERNET` no `AndroidManifest.xml` e realiza as operações localmente no aparelho.

## Créditos e licença

O SINAPSE Crypto é distribuído sob a licença MIT. A compatibilidade implementada foi baseada no comportamento do projeto open source **android-hidden-aes**, de Roberto Xavier Collura, também licenciado sob MIT. Consulte [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).


### Interface 1.0.0

O **Resultado** é somente leitura, não recebe foco de edição e não abre o teclado. A área contém apenas o texto produzido e o botão **Copiar**. O **Texto de Entrada** mantém o editor em tela cheia.
