---
title: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Ação
description: Ativação de Segmento para o Hub de Eventos do Microsoft Azure - Ação
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 Cenário completo

## 13.6.1 Iniciar o acionador do Hub de Eventos do Azure

Para mostrar o payload enviado pela CDP em tempo real do Adobe Experience Platform para nosso Hub de eventos do Azure na qualificação do segmento, precisamos iniciar nossa função de acionador do Hub de eventos do Azure. Esta função irá simples &quot;despejar&quot; a carga para o console no Visual Studio Code. Mas lembre-se de que essa função pode ser estendida de qualquer maneira para fazer interface com todos os tipos de ambientes usando APIs e protocolos dedicados.

### Inicie o Visual Studio Code e inicie o projeto

Certifique-se de que seu projeto do Visual Studio Code esteja aberto e em execução

Para iniciar/parar/reiniciar sua função do Azure no Visual Studio Code, consulte os seguintes exercícios:

- [Exercício 13.5.4 - Iniciar Projeto Azure](./ex5.md)
- [Exercício 13.5.5 - Parar Projeto Azure](./ex5.md)

Seu código do Visual Studio **Terminal** O deve mencionar algo semelhante a isto:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Carregar o site do Luma

Ir para [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Depois de fazer logon com sua Adobe ID, você verá isso. Clique no projeto do seu site para abri-lo.

![DSN](../module0/images/web8.png)

Agora você pode seguir o fluxo abaixo para acessar o site. Clique em **Integrações**.

![DSN](../module0/images/web1.png)

No **Integrações** , é necessário selecionar a propriedade Data Collection criada no exercício 0.1.

![DSN](../module0/images/web2.png)

Você verá seu site de demonstração aberto. Selecione o URL e copie-o para a área de transferência.

![DSN](../module0/images/web3.png)

Abra uma nova janela incógnita do navegador.

![DSN](../module0/images/web4.png)

Cole o URL do site de demonstração, que você copiou na etapa anterior. Em seguida, você será solicitado a fazer logon usando sua Adobe ID.

![DSN](../module0/images/web5.png)

Selecione o tipo de conta e conclua o processo de logon.

![DSN](../module0/images/web6.png)

Você verá seu site carregado em uma janela incógnita do navegador. Para cada demonstração, você precisará usar uma nova janela incógnita do navegador para carregar o URL do site de demonstração.

![DSN](../module0/images/web7.png)

## 13.6.3 Qualifique-se para o seu segmento Interesse em equipamento

Navegue até o **Equipamento** uma vez, e **não recarregue nem atualize**. Essa ação deve qualificá-lo para `--demoProfileLdap-- - Interest in Equipment` segmento.

![6-04-luma-telco-nav-Sports.png](./images/luma1.png)

Para verificar, abra o painel Visualizador de perfil. Agora você deve ser um membro do `--demoProfileLdap-- - Interest in Equipment`. Se as associações de segmento ainda não tiverem sido atualizadas no painel Visualizador de perfil, clique no botão Recarregar .

![6-05-luma-telco-nav-band.png](./images/luma2.png)

Volte para o Visual Studio Code e olhe para seu **TERMINAL** , você deve ver uma lista de segmentos para seu **ECID**. Essa carga de ativação é entregue ao seu hub de eventos assim que você se qualifica para a variável `--demoProfileLdap-- - Interest in Equipment` segmento.

Ao observar mais de perto a carga do segmento, você pode ver que `--demoProfileLdap-- - Interest in Equipment` está no status **realizado**.

Um status de segmento de **realizado** significa que o perfil acabou de entrar no segmento. Enquanto a variável **existente** status significa que o perfil continua no segmento.

![6-06-vsc-ativation-percebido.png](./images/luma3.png)

## 13.6.4 Visite a página Equipamento pela segunda vez

Faça uma atualização rígida do **Equipamento** página.

![6-07-back-to-Sports.png](./images/luma1.png)

Agora, volte para o Código do Visual Studio e verifique seu **TERMINAL** guia . Você verá que ainda temos seu segmento, mas agora em status **existente** o que significa que nosso perfil continua no segmento.

![6-08-vsc-ativation-existing.png](./images/luma4.png)

## 13.6.5 Visite a página Esportes por uma terceira vez

Se você revisitar o **Esportes** por uma terceira vez, nenhuma ativação ocorrerá, pois não há alteração de estado do ponto de vista de um segmento.

As ativações de segmento ocorrem apenas quando o status do segmento muda:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Próxima etapa: [Resumo e benefícios](./summary.md)

[Voltar ao Módulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Voltar para todos os módulos](./../../overview.md)
