---
title: Adobe Journey Optimizer - API de clima externa, Ação de SMS e muito mais - Definir uma fonte de dados externa
description: Adobe Journey Optimizer - API de clima externa, Ação de SMS e muito mais - Definir uma fonte de dados externa
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 3%

---

# 3.2.2 Definir uma fonte de dados externa

Neste exercício, você criará uma fonte de dados externa personalizada usando o Adobe Journey Optimizer.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Para alterar a sandbox, clique em **Produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **AEP Enablement FY22**. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** em **Fontes de Dados**.

![Demonstração](./images/menudatasources.png)

Você verá a lista **Fontes de Dados**.
Clique em **Criar Source de Dados** para começar a adicionar sua fonte de dados.

![Demonstração](./images/dshome.png)

Você verá um pop-up vazio da fonte de dados.

![Demonstração](./images/emptyds.png)

Antes de começar a configurar isso, você precisará de uma conta com o serviço **Abrir Mapa Meteorológico**. Siga estas etapas para criar sua conta e obter sua chave de API.

Ir para [https://openweathermap.org/](https://openweathermap.org/). Na página inicial, clique em **Entrar**.

![MapaMeteorológico](./images/owm.png)

Clique em **Criar uma Conta**.

![MapaMeteorológico](./images/owm1.png)

Preencha os detalhes.

![MapaMeteorológico](./images/owm2.png)

Clique em **Criar Conta**.

![MapaMeteorológico](./images/owm3.png)

Você será redirecionado para a Página da sua conta.

![MapaMeteorológico](./images/owm4.png)

No menu, clique em **Chaves de API** para recuperar sua Chave de API, que você precisará para configurar sua fonte de dados externa personalizada.

![MapaMeteorológico](./images/owm5.png)

Uma **Chave de API** tem esta aparência: `b2c4c36b6bb59c3458d6686b05311dc3`.

Você pode encontrar a **Documentação da API** para a **Previsão atual** [aqui](https://openweathermap.org/current).

No nosso caso de uso, implementaremos a conexão com o Open Weather Map com base na cidade em que o cliente está.

![MapaMeteorológico](./images/owm6.png)

Volte para o **Adobe Journey Optimizer**, para o pop-up **External Data Source** vazio.

![Demonstração](./images/emptyds.png)

Como um Nome para a fonte de dados, use `--aepUserLdap--WeatherApi`. Neste exemplo, o Nome da fonte de dados é `vangeluwWeatherApi `.

Defina a Descrição como: `Access to the Open Weather Map`.

A URL para a API Abrir Mapa Meteorológico é: **http://api.openweathermap.org/data/2.5/weather?units=metric**

![Demonstração](./images/dsname.png)

Em seguida, é necessário selecionar a Autenticação a ser usada.

Use estas variáveis:

| Campo | Valor |
|:-----------------------:| :-----------------------|
| Tipo | **Chave de API** |
| Nome | **APPID** |
| Valor | **sua chave de API** |
| Localização | **Parâmetro de consulta** |

![Demonstração](./images/dsauth.png)

Finalmente, você precisa definir um **FieldGroup**, que é basicamente a solicitação que você enviará para a API do clima. Em nosso caso, queremos usar o nome da cidade para solicitar o Tempo Atual para essa cidade.

![Demonstração](./images/fg.png)

De acordo com a Documentação da API de Tempo, precisamos enviar um parâmetro `q=City`.

![Demonstração](./images/owmapi.png)

Para corresponder à Solicitação de API esperada, configure seu FieldGroup da seguinte maneira:

>[!IMPORTANT]
>
>O nome do grupo de campos deve ser exclusivo. Use esta convenção de nomenclatura: `--aepUserLdap--WeatherByCity`. Nesse caso, o nome deve ser `vangeluwWeatherByCity`

![Demonstração](./images/fg1.png)

Para a Carga de resposta, é necessário colar um exemplo da Resposta que será enviada pela API de Tempo.

Você pode encontrar a Resposta JSON da API esperada na página Documentação da API [aqui](https://openweathermap.org/current).

![Demonstração](./images/owmapi1.png)

Ou você pode copiar a Resposta JSON daqui:

```json
{"coord": { "lon": 139,"lat": 35},
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 281.52,
    "feels_like": 278.99,
    "temp_min": 280.15,
    "temp_max": 283.71,
    "pressure": 1016,
    "humidity": 93
  },
  "wind": {
    "speed": 0.47,
    "deg": 107.538
  },
  "clouds": {
    "all": 2
  },
  "dt": 1560350192,
  "sys": {
    "type": 3,
    "id": 2019346,
    "message": 0.0065,
    "country": "JP",
    "sunrise": 1560281377,
    "sunset": 1560333478
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
  "cod": 200
}
```

Copie a Resposta JSON acima para a área de transferência e vá para a tela de configuração da fonte de dados personalizada.

Clique no ícone **Editar Carga**.

![Demonstração](./images/owmapi2.png)

Você verá um pop-up no qual terá que colar a Resposta JSON acima.

![Demonstração](./images/owmapi3.png)

Cole sua resposta JSON, e você verá isso depois. Clique em **Salvar**.

![Demonstração](./images/owmapi4.png)

A configuração da fonte de dados personalizada está concluída. Role para cima e clique em **Salvar**.

![Demonstração](./images/dssave.png)

Sua fonte de dados foi criada com êxito e faz parte da lista **Fontes de Dados**.

![Demonstração](./images/dslist.png)

Próxima Etapa: [3.2.3 Definir uma ação personalizada](./ex3.md)

[Voltar ao módulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Voltar a todos os módulos](../../../overview.md)
