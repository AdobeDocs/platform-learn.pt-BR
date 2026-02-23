---
title: Cursor e servidores MCP AEM
description: Cursor e servidores MCP AEM
kt: 5342
doc-type: tutorial
source-git-commit: 1abfd8d1f270a810dd65d9921c69834df2a9147d
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# 1.6.2 Servidores e cursor do AEM MCP

>[!IMPORTANT]
>
>Para concluir este exercício, você precisa ter acesso a um ambiente de trabalho do AEM Sites e do Assets CS com EDS e os vários agentes do AEM precisam estar habilitados para a organização IMS que você está usando.
>
>Se você ainda não tiver esse ambiente, vá para o exercício [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga as instruções aqui e você terá acesso a esse ambiente.

>[!IMPORTANT]
>
>Se você configurou anteriormente um programa do AEM CS com um ambiente do AEM Sites e do Assets CS, pode ser que sua sandbox do AEM CS tenha hibernado. Considerando que a deshibernação de uma sandbox desse tipo leva de 10 a 15 minutos, seria uma boa ideia iniciar o processo de deshibernação agora para que você não precise aguardar mais tarde.


Estes são todos os servidores MCP do AEM disponíveis:

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly (operações de conteúdo somente leitura)
- https://mcp.adobeaemcloud.com/adobe/mcp/content-updater (expõe a habilidade correspondente do Agente de produção de experiência)
- https://mcp.adobeaemcloud.com/adobe/mcp/experience-governance (Expõe as habilidades para obter e verificar a política de marca de uma página)
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery (expõe habilidades para descobrir conteúdo em um ambiente do AEM)

Neste exercício, você encontrará instruções sobre como usar esses servidores MCP específicos:

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery

Você pode usar as instruções abaixo para configurar servidores MCP semelhantes para os outros servidores MCP AEM disponíveis, pois o processo é muito semelhante.

## Configuração do Servidor MCP do Cursor do Agente de Produção de Experiência 1.6.2.1

Cria uma nova pasta vazia na área de trabalho.

![Cursor + AEM](./images/cursorai1.png)

Abrir cursor. Clique em **Abrir projeto**.

![Cursor + AEM](./images/cursorai2.png)

Selecione a pasta criada anteriormente e clique em **Abrir**.

![Cursor + AEM](./images/cursorai3.png)

Clique em **Sim, eu confio nos autores**.

![Cursor + AEM](./images/cursorai4.png)

Você deverá ver isso. Use o atalho de teclado `Cmd + Shift + J` para abrir as configurações do Cursor. Você deverá ver isso. Ir para **Ferramentas&amp; MCP**.

![Cursor + AEM](./images/cursorai5.png)

Clique em **+ Novo servidor MCP**.

![Cursor + AEM](./images/cursorai6.png)

Adicione o seguinte servidor MCP ao arquivo **mcp.json**. Pode haver outros Servidores MCP já especificados nesse arquivo - não os remova e adicione apenas as novas linhas abaixo. Salve as alterações.

```json
"aem": {
	"url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
	}
```

![Cursor + AEM](./images/cursorai7.png)

Volte para a guia **Configurações do cursor**. Agora você deve ver uma ferramenta chamada **aem** adicionada à lista de servidores MCP. Clique em **conectar** para autenticar usando sua conta da Adobe.

![Cursor + AEM](./images/cursorai8.png)

Clique em **Abrir** caso veja esta mensagem. Em seguida, você deve autenticar no navegador.

![Cursor + AEM](./images/cursorai9.png)

Após a autenticação bem-sucedida, você verá algo como isso.

![Cursor + AEM](./images/cursorai10.png)

Feche as guias **Configurações do cursor** e **mcp.json**. Cole o seguinte prompt no chat e clique em **enviar**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Cursor + AEM](./images/cursorai11.png)

Clique em **Executar**.

![Cursor + AEM](./images/cursorai12.png)

Você deverá ver uma resposta semelhante.

![Cursor + AEM](./images/cursorai13.png)

![Cursor + AEM](./images/cursorai14.png)

Como você pode ver, recursos semelhantes são expostos por meio do servidor MCP no Cursor em comparação ao que foi possível usando o Assistente de IA no exercício anterior.

Digite o prompt a seguir e clique em **Enviar**.

```javascript
List AEM Author instances
```

![Cursor + AEM](./images/cursorai15.png)

Você deveria ver algo assim. Procure o ambiente que deseja usar, insira o seguinte prompt e clique em **Enviar**.

```javascript
use environment number X
```

![Cursor + AEM](./images/cursorai16.png)

Você deverá ver isso.

![Cursor + AEM](./images/cursorai17.png)

Cole o prompt a seguir e clique em **enviar**. Substitua XXX nesse prompt pelo URL copiado no exercício anterior.

```
On the page https://author-p185022-e1936676.adobeaemcloud.com/content/CitiSignal/fiber-max.html, please make the following changes:

- change the word 'winter' to 'summer'
- change the text 'be as fast as a leopard' to 'dominate your internet like a gorilla'
- change the image in the hero block to use the image 'citisignal_gorilla.png'
- change the text '99.9% network reliability' to '99.998% network reliability'
```

![Cursor + AEM](./images/cursorai18.png)

Após 1-2 minutos, você deverá obter uma resposta semelhante. Copie o URL e abra a página no navegador.

![Cursor + AEM](./images/cursorai19.png)

Você deverá ver isso.

![Cursor + AEM](./images/cursorai20.png)

Digite o prompt a seguir e clique em **Enviar**.

```javascript
promote the changes by creating a new launch and promoting it
```

![Cursor + AEM](./images/cursorai21.png)

Após 1-2 minutos, as alterações são promovidas.

![Cursor + AEM](./images/cursorai22.png)

Agora você pode ver as alterações em tempo real no seu site.

![Cursor + AEM](./images/cursorai23.png)

Sinta-se à vontade para explorar os outros recursos do servidor MCP AEM.

## Instalação do Servidor MCP do Cursor do Agente de Descoberta 1.6.2.2

Use o atalho de teclado `Cmd + Shift + J` para abrir as configurações do Cursor. Você deverá ver isso. Ir para **Ferramentas&amp; MCP**. Clique em **+ Novo servidor MCP**.

![Cursor + AEM](./images/cursoraiz5.png)

Adicione o seguinte servidor MCP ao arquivo **mcp.json**. Pode haver outros Servidores MCP já especificados nesse arquivo - não os remova e adicione apenas as novas linhas abaixo. Salve as alterações.

```
,
"aem-discovery": {
	"url": "https://mcp.adobeaemcloud.com/adobe/mcp/discovery"
}
```

![Cursor + AEM](./images/cursoraiz7.png)

Volte para a guia **Configurações do cursor**. Agora você deve ver uma ferramenta chamada **aem** adicionada à lista de servidores MCP. Clique em **conectar** para autenticar usando sua conta da Adobe.

![Cursor + AEM](./images/cursoraiz8.png)

Após a autenticação, você deve ver isso.

![Cursor + AEM](./images/cursoraiz9.png)

Feche as guias **Configurações do cursor** e **mcp.json**. Cole o seguinte prompt no chat e clique em **enviar**.

```
I just created a new custom mcp server named 'aem-discovery'. what can I do with that?
```

![Cursor + AEM](./images/cursoraiz10.png)

```
for the environment https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/, list all assets tagged with 'Spring 2026'
```

![Cursor + AEM](./images/cursoraiz11.png)

Você deveria ver algo assim.

![Cursor + AEM](./images/cursoraiz12.png)

## Próximas etapas

Voltar para [AEM e Agentes](./aemagents.md){target="_blank"}

[Voltar para Todos os Módulos](./../../../overview.md){target="_blank"}