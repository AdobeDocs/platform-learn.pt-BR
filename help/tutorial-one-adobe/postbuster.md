---
title: PostBuster - Funcionários do Adobe
description: PostBuster - Funcionários do Adobe
doc-type: multipage-overview
exl-id: 01e30878-e1a9-4f46-bcf2-0074686ec1b5
source-git-commit: 54303033e23a28c45e9ef6c7a85135b21b3e29dc
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>As instruções a seguir são destinadas apenas aos funcionários da Adobe.

## Instalar PostBuster

Ir para [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Clique para baixar a versão mais recente do **PostBuster**.

![PostBuster](./assets/images/pb1.png)

Baixe a versão correta para seu sistema operacional.

![PostBuster](./assets/images/pb2.png)

Depois que o download for concluído e instalado, abra o PostBuster. Você deverá ver isso. Clique em **Importar**.

![PostBuster](./assets/images/pb3.png)

Baixe o [postbuster.json.zip](./assets/postman/postbuster.json.zip) e extraia-o na sua área de trabalho.

![PostBuster](./assets/images/pbpb.png)

Clique em **Escolher um Arquivo**.

![PostBuster](./assets/images/pb4.png)

Selecione o arquivo **postbuster.json**. Clique em **Abrir**.

![PostBuster](./assets/images/pb5.png)

Você deverá ver isso. Clique em **Verificar**.

![PostBuster](./assets/images/pb6.png)

Clique em **Importar**.

![PostBuster](./assets/images/pb7.png)

Você deverá ver isso. Clique em para abrir a coleção importada.

![PostBuster](./assets/images/pb8.png)

Agora você vê sua coleção. Você ainda precisa configurar um ambiente para manter algumas variáveis de ambiente.

![PostBuster](./assets/images/pb9.png)

Clique em **Ambiente base** e no ícone **editar**.

![PostBuster](./assets/images/pb10.png)

Você deverá ver isso.

![PostBuster](./assets/images/pb11.png)

Copie o espaço reservado do ambiente abaixo e cole-o no **Ambiente base**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

Você deveria ficar com isso.

![PostBuster](./assets/images/pb12.png)

Depois de passar pelo módulo **Firefly Services**, seu ambiente deve ficar assim. Você não precisa fazer isso agora. Isso será abordado em um estágio posterior.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Informantes técnicos](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Em caso de dúvidas, envie um email para **techinsiders@adobe.com** para compartilhar comentários gerais sobre sugestões para conteúdo futuro. Entre em contato diretamente com o Tech Insiders.

[Voltar a todos os módulos](./overview.md)
