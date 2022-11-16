---
title: Adobe Journey Optimizer - API de Tempo Externo, Ação de SMS e muito mais - Defina uma fonte de dados externa
description: Adobe Journey Optimizer - API de Tempo Externo, Ação de SMS e muito mais - Defina uma fonte de dados externa
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: e3e04415-4258-4ad7-a227-0e68dfcba235
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 4%

---

# 8.2 Definir uma fonte de dados externa

Neste exercício, você criará uma fonte de dados externa personalizada usando o Adobe Journey Optimizer.

Faça logon no Adobe Journey Optimizer acessando [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Você será redirecionado para o **Início**  no Journey Optimizer. Primeiro, certifique-se de usar a sandbox correta. A sandbox a ser usada é chamada de `--aepSandboxId--`. Para alterar de uma sandbox para outra, clique em **Produto de produção (VA7)** e selecione a sandbox na lista. Neste exemplo, a sandbox é chamada de **Ativação AEP FY22**. Você estará no **Início** exibição da sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

No menu esquerdo, role para baixo e clique em **Configurações**. Em seguida, clique no botão **Gerenciar** botão abaixo **Fontes de dados**.

![Demonstração](./images/menudatasources.png)

Você verá o **Fontes de dados** lista.
Clique em **Criar fonte de dados** para começar a adicionar a fonte de dados.

![Demonstração](./images/dshome.png)

Você verá um pop-up de fonte de dados vazio.

![Demonstração](./images/emptyds.png)

Antes de começar a configurar isso, você precisará de uma conta com o **Abrir mapa de clima** serviço. Siga estas etapas para criar sua conta e obter a chave de API.

Ir para [https://openweathermap.org/](https://openweathermap.org/). Na página inicial, clique em **Fazer logon**.

![WeatherMap](./images/owm.png)

Clique em **Criar uma conta**.

![WeatherMap](./images/owm1.png)

Preencha os detalhes.

![WeatherMap](./images/owm2.png)

Clique em **Criar conta**.

![WeatherMap](./images/owm3.png)

Em seguida, você será redirecionado para a sua Página da conta.

![WeatherMap](./images/owm4.png)

No menu, clique em **Chaves de API** para recuperar a chave de API, que será necessário configurar a fonte de dados externa personalizada.

![WeatherMap](./images/owm5.png)

Um **Chave da API** tem esta aparência: `b2c4c36b6bb59c3458d6686b05311dc3`.

Você pode encontrar a variável **Documentação da API** para **Tempo atual** [here](https://openweathermap.org/current).

No nosso caso de uso, implementaremos a conexão com o Open Weather Map com base na cidade em que o cliente está.

![WeatherMap](./images/owm6.png)

Volte para **Adobe Journey Optimizer**, em seu vazio **Fonte de Dados Externa** pop-up.

![Demonstração](./images/emptyds.png)

Como um Nome para a fonte de dados, use `--demoProfileLdap--WeatherApi`. Neste exemplo, o Nome da fonte de dados é `vangeluwWeatherApi `.

Defina Descrição como: `Access to the Open Weather Map`.

O URL para a API do mapa de tempo aberto é: **http://api.openweathermap.org/data/2.5/weather?units=metric**

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

Por fim, é necessário definir um **FieldGroup**, que é basicamente a solicitação que você enviará para a API do tempo. No nosso caso, queremos usar o nome da Cidade para solicitar o Tempo Atual para aquela Cidade.

![Demonstração](./images/fg.png)

De acordo com a Documentação da API do tempo, precisamos enviar um parâmetro `q=City`.

![Demonstração](./images/owmapi.png)

Para corresponder à Solicitação de API esperada, configure o FieldGroup da seguinte maneira:

>[!IMPORTANT]
>
>O nome do grupo de campos deve ser exclusivo. Use esta convenção de nomenclatura: `--demoProfileLdap--WeatherByCity` nesse caso, o nome deve ser `vangeluwWeatherByCity`

![Demonstração](./images/fg1.png)

Para a Carga de Resposta, é necessário colar um exemplo da Resposta que será enviada pela API de Tempo.

Você pode encontrar a resposta JSON da API esperada na página Documentação da API [here](https://openweathermap.org/current).

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

Copie a resposta JSON acima para a área de transferência e vá para a tela de configuração personalizada da fonte de dados.

Clique no botão **Editar carga** ícone .

![Demonstração](./images/owmapi2.png)

Você verá um pop-up em que agora precisa colar a Resposta JSON acima.

![Demonstração](./images/owmapi3.png)

Cole a resposta JSON, depois disso você verá isso. Clique em **Salvar**.

![Demonstração](./images/owmapi4.png)

A configuração personalizada da fonte de dados foi concluída. Role para cima e clique **Salvar**.

![Demonstração](./images/dssave.png)

Sua fonte de dados agora foi criada com êxito e faz parte do **Fontes de dados** lista.

![Demonstração](./images/dslist.png)

Próxima etapa: [8.3 Definir uma ação personalizada](./ex3.md)

[Voltar ao Módulo 8](journey-orchestration-external-weather-api-sms.md)

[Voltar para todos os módulos](../../overview.md)
