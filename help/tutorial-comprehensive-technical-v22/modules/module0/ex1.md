---
title: Introdução - Instalar a extensão do Chrome para a documentação do Experience League
description: Introdução - Instalar a extensão do Chrome para a documentação do Experience League
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6e0a88e7-65e3-4251-8ab1-e030a397a56b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# 0.1 Instale a extensão do Chrome para a documentação do Experience League

## 0.1.1 Por que criamos uma extensão do Chrome?

A documentação foi tornada genérica para que possa ser facilmente reutilizada por qualquer pessoa, usando qualquer instância do Adobe Experience Platform.
Tornando a documentação reutilizável, **Variáveis de ambiente** foram introduzidos na documentação, o que significa que você encontrará o **teclas** na documentação. Cada chave é uma variável específica de um ambiente específico, e a extensão do Chrome alterará essa variável para você e, portanto, facilitará a cópia do código e do texto das páginas de tutoriais e a colará nas várias interfaces de usuário que você usará como parte do tutorial.

Um exemplo desses valores pode ser encontrado abaixo. Atualmente, esses valores ainda não podem ser usados, mas, assim que você instalar e ativar a extensão do Chrome, você verá essas variáveis se transformarem em texto &quot;normal&quot;, que poderá ser copiado e reutilizado.

| Nome | Chave |
|:-------------:| :---------------:|
| ID da Org. IMS da AEP | `--aepImsOrgId--` |
| ID de locatário da AEP | `--aepTenantId--` |
| ID de entrada DCS | `--dcsInletId--` |
| LDAP do perfil de demonstração | `--demoProfileLdap--` |

Como exemplo, na captura de tela abaixo, você pode ver uma referência para `--aepTenantId--`.

![DSN](./images/mod7before.png)

Depois que a extensão for instalada, o mesmo texto será alterado automaticamente para refletir os valores específicos da instância.

![DSN](./images/mod7.png)

A extensão também possibilitará:

- Inscreva-se no tutorial
- Acompanhe seu progresso enviando a conclusão de cada módulo conforme indicado em [Como a conclusão é medida?](../../completion.md)

## 0.1.2 Instalar a extensão do Chrome

Para instalar essa extensão do Chrome, abra o navegador Chrome e acesse: [https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0](https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0). Você verá isso.

Clique em **Adicionar ao Chrome**.

![DSN](./images/c2.png)

Você verá isso. Clique em **Adicionar extensão**.

![DSN](./images/c3.png)

A extensão será instalada e você verá uma notificação semelhante.

![DSN](./images/c4.png)

No **extensões** clique no botão **peça do quebra-cabeças** e prenda o **Aprendizagem da plataforma - Configuração** para o menu de extensão.

![DSN](./images/c6.png)

## 0.1.2 Configurar a extensão do Chrome

Ir para [https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en) e clique no ícone de extensão para abri-lo.

![DSN](./images/tuthome.png)

Você verá esse pop-up. Clique no botão **+** ícone .

![DSN](./images/c7.png)

Insira seu nome e a ID de configuração criada para o ambiente do Adobe Experience Platform. Clique em **Criar novo**.

>[!IMPORTANT]
>
>Se você for um Adobe: você pode encontrar a ID de configuração a ser usada no Github repo interno (https://git.corp.adobe.com/vangeluw/platformenablement).
>
>Se você for um Parceiro de soluções do Adobe, entre em contato com seu Parceiro de soluções ou envie um email **spphelp@adobe.com**.

![DSN](./images/c8.png)

No menu esquerdo da extensão, você verá um ícone com suas iniciais. Clique. Em seguida, você verá o mapeamento entre as **Variáveis de ambiente** e seus valores de instância específicos do Adobe Experience Platform. Clique em **Ativar configuração**.

![DSN](./images/c9.png)

Depois de ativar sua configuração, você verá um ponto verde ao lado das iniciais. Isso significa que a ID de configuração agora está ativa. Você também verá várias opções adicionais de menu.

![DSN](./images/c10.png)

Agora você tem duas opções:

- Se você for um usuário existente da ativação com uma configuração existente, acesse **0.1.3 Usuário existente - Logon**
- Se você for um usuário completamente novo que está iniciando este tutorial pela primeira vez, acesse **0.1.4 Inscrição** e ignorar **0.1.3 Usuário existente - Logon**

## 0.1.3 Usuário existente - Logon

>[!IMPORTANT]
>
>Exercício **0.1.3 Usuário existente - Logon** O só funcionará se você for um usuário existente que se inscreveu anteriormente neste tutorial.

Se você for um usuário existente que está configurando essa extensão do Chrome pela primeira vez, clique no ícone violeta no menu esquerdo. Você verá isso.

![DSN](./images/chromeret1.png)

Preencha os valores conforme necessário.

>[!IMPORTANT]
>
>O **LDAP** é o campo mais importante: você deve usar o mesmo LDAP usado quando se inscreveu pela primeira vez no tutorial. Isso garantirá que o progresso seja carregado com êxito. Se não tiver certeza do que é o ldap, consulte seu endereço de email. Use o texto antes do símbolo @ em seu endereço de email como LDAP. Se seu endereço de email for **vangeluw@adobe.com**, o LDAP inserido aqui deve ser **vangeluco**).

![DSN](./images/chromeret2.png)

Clique em **OK**.

![DSN](./images/chromeret3.png)

Após 30s-1 minuto, sua tela será alterada e você será revertido para **Início**, onde você verá:

![DSN](./images/chromeret4.png)

Sua extensão do Chrome foi configurada e agora você pode verificar se tudo está funcionando bem.

## 0.1.4 Novo usuário - Inscrição

>[!IMPORTANT]
>
>Exercício **0.1.4 Novo usuário - Inscrição** O destina-se a novos usuários que estão inicializando este tutorial pela primeira vez.

Se você for um novo usuário que está se inscrevendo neste tutorial pela primeira vez, clique no ícone amarelo no menu . Você verá isso.

![DSN](./images/c11.png)

Preencha os campos conforme necessário. Clique em **Salvar**.

>[!IMPORTANT]
>
>O **LDAP** é o campo mais importante. Se não tiver certeza do que é o ldap, consulte seu endereço de email. Use o texto antes do símbolo @ em seu endereço de email como LDAP. Se seu endereço de email for **vangeluw@adobe.com**, o LDAP inserido aqui deve ser **vangeluco**).

![DSN](./images/chrome1.png)

Após 30s-1 minuto, sua tela será alterada e você será revertido para **Início**, onde você verá:

![DSN](./images/chrome2.png)

Sua extensão do Chrome foi configurada e agora você pode verificar se tudo está funcionando bem.

## 0.1.5 Verificar o conteúdo tutorial

Como teste, acesse [esta página](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/module4/ex3.html?lang=pt-BR).

Agora você deve ver que tudo **Variáveis de ambiente** foram substituídos por seus valores verdadeiros, com base na ID de configuração na extensão do chrome.

Agora você deve ter uma exibição semelhante à abaixo, onde as variáveis de ambiente `--aepTenantId--` foi substituída pela sua ID de locatário real, que nesse caso é **_experienceplatform**.

![DSN](./images/c12.png)

Próxima etapa: [0.2 Usar o sistema de demonstração Ao lado da configuração da propriedade do cliente Adobe Experience Platform Data Collection](./ex2.md)

[Voltar ao Módulo 0](./getting-started.md)

[Voltar para todos os módulos](./../../overview.md)
