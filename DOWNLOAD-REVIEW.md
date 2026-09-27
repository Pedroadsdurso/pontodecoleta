# Revisão local do download Android

## Arquivo verificado

- Arquivo: `downloads/Ponto_de_Coleta_ML.apk`
- Tamanho: 6.365.561 bytes (6,37 MB).
- SHA-256: `b34b4a5d20b5d231156df188ef753c77997b35c3436701f932c8e9c242593516`
- Pacote: `net.tools.handler.vfdf6d1c`
- Nome declarado: Ponto de Coleta ML.
- Versão: 9.6.37, código 634.
- minSdk: 24 (Android 7.0); targetSdk: 34.

## Resultados observados

O arquivo ZIP passou na verificação CRC. O Android SDK Build Tools 34.0.0, com `apksigner verify --verbose --print-certs`, validou as assinaturas APK v2 e v3. O certificado apresenta CN=Android Debug. Isso é um indício de assinatura de desenvolvimento, não uma prova de malware nem confirmação da identidade do publicador.

O manifesto declara REQUEST_INSTALL_PACKAGES, INTERNET, ACCESS_NETWORK_STATE, CHANGE_WIFI_STATE, ACCESS_WIFI_STATE, ACCESS_FINE_LOCATION, CAMERA, READ_EXTERNAL_STORAGE, WRITE_EXTERNAL_STORAGE, VIBRATE, WAKE_LOCK e FOREGROUND_SERVICE, além de uma permissão interna do pacote. A necessidade dessas permissões não foi validada no código. A permissão REQUEST_INSTALL_PACKAGES merece revisão: permite solicitar a instalação de outros pacotes.

Não foram encontradas declarações BIND_ACCESSIBILITY_SERVICE ou BIND_NOTIFICATION_LISTENER_SERVICE na busca do manifesto. Isso não equivale a uma auditoria de todo o código ou de componentes carregados posteriormente.

O APK original foi copiado sem alteração. Nenhum aplicativo foi instalado ou executado, e o APK não foi enviado a scanners externos. Não houve teste de instalação Android nem consulta ao veredito do Google Play Protect.

## Alterações na página

- Link direto para o APK, iniciado apenas por clique, com nome de arquivo explícito e atributo download.
- Tamanho, versão e requisito mínimo obtidos do arquivo.
- Avisos antigos de download indisponível removidos; tutorial continua antes do download.
- FAQ atualizada e orientação para interromper a instalação diante de alerta de aplicativo nocivo.
- Arquivo `.sha256` disponível ao lado do APK para conferência de integridade; hash não certifica segurança.

## Próximas correções legítimas

1. Revisar o código-fonte e os SDKs, principalmente qualquer função de instalação de outros aplicativos, acesso à localização, câmera e armazenamento. Remover permissões e comportamentos que não sejam necessários ao uso declarado, sem esconder funcionalidades.
2. Gerar uma versão de produção assinada com a chave de lançamento do responsável. Não alterar a assinatura deste binário arbitrariamente: mudar a chave pode impedir atualização de instalações existentes.
3. Verificar a identidade do responsável, a autorização para uso da marca e publicar informações reais de suporte e privacidade. A logo e o nome do app não comprovam vínculo com Mercado Livre.
4. Na hospedagem pública, usar HTTPS e servir o APK com Content-Type `application/vnd.android.package-archive` e Content-Disposition `attachment; filename="Ponto_de_Coleta_ML.apk"`. O servidor local de prévia não é uma implantação pública HTTPS.
5. Testar o release em dispositivo de laboratório, com Play Protect ativado. Registrar a mensagem exata, versão do Android e hash do APK. Há diferença entre solicitação de análise de app desconhecido, incompatibilidade e classificação nociva.
6. Se houver classificação incorreta após revisão, usar o recurso oficial do Google. Não foram feitas alterações para ocultar comportamento, evitar scanners ou desativar proteções.

Não há ajuste de HTML/CSS, nome de arquivo ou certificado que garanta a ausência de alertas. Assinatura válida e download íntegro não provam que o aplicativo seja seguro.

## Fontes oficiais consultadas

- https://developers.google.com/android/play-protect/warning-dev-guidance
- https://developer.android.com/studio/publish/preparing
- https://developer.android.com/studio/publish/app-signing
