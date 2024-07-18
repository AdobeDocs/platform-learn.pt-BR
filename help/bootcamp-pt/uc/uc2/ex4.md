---
title: Bootcamp - Journey Optimizer Crie sua jornada - Brasil
description: Bootcamp - Journey Optimizer Crie sua jornada - Brasil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 674a9baa-5900-405e-b744-ea211f60a16d
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---

# 2.4 Testa sua jornada

## Fluxo da jornada do cliente

Abra uma nova e anônima do navegador e vá para [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir tudo**. Com base no seu comportamento de navegação no fluxo de dados anterior, verá a personalização na página inicial do site.

![DSN](./images/web8a.png)

Clique no ➡ **Perfil** sem canto superior direito da tela.

![Demonstração](./images/web8b.png)

Clique em **Criar uma conta**.

![Demonstração](./images/pv5.png)

Preencha todos os campos do campo. Use um valor real para endereço de e-mail e número de telefone, pois usado em para envio de e-mail SMS.

![Demonstração](./images/pv7a.png)

Função para baixo. Agora você deve o eventoID do seu evento personalizado que criou no exercício 2.2. Você pode encontrar-lo aqui:

![ACOP](./images/payloadeventID.png)

O eventID é o que precisa ser enviado à Adobe Experience Platform para acionar a jornada que você perdeu. Este é o eventID exemplo:
`19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Preencha o eventID no campo **ID do Evento de Criação de Conta** e clique em **Registrar**.

![Demonstração](./images/pv8a.png)

Em seguida, a tela abaixo é apresentada:

![Demonstração](./images/pv9.png)

Você também recebe este e-mail, que é o e-mail que é mesmo criado como parte deste exercício.

![Demonstração](./images/pv10a.png)

Você terminou este exercício.

Próxima etapa: [2.5 Instale e use o móvel](./ex5.md)

[Retorno para Fluxo de monitoramento 2](./uc2.md)

[Retorno para Todos os compartilhados](../../overview.md)
