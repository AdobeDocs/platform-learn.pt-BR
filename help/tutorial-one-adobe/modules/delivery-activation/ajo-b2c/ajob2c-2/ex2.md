---
title: Adobe Journey Optimizer - API de clima externa, Ação de SMS e muito mais - Definir uma fonte de dados externa
description: Adobe Journey Optimizer - API de clima externa, Ação de SMS e muito mais - Definir uma fonte de dados externa
kt: 5342
doc-type: tutorial
exl-id: 0ad27ffb-51fe-4bd1-b0be-feeb232039fa
source-git-commit: d19bd2e39c7ff5eb5c99fc7c747671fb80e125ee
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 4%

---

# 3.2.2 Definir uma fonte de dados externa

Neste exercício, você criará uma fonte de dados externa personalizada usando o Adobe Journey Optimizer.

Faça login no Adobe Journey Optimizer em [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Você será redirecionado para a exibição **Página inicial** no Journey Optimizer. Primeiro, verifique se você está usando a sandbox correta. A sandbox a ser usada é chamada `--aepSandboxName--`. Você estará na exibição **Página inicial** da sua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

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

Preencha os detalhes. Clique em **Criar Conta**.

![MapaMeteorológico](./images/owm2.png)

Você será redirecionado para a Página da sua conta.

![MapaMeteorológico](./images/owm4.png)

No menu, clique em **Chaves de API** para recuperar sua Chave de API, que você precisará para configurar sua fonte de dados externa personalizada.

![MapaMeteorológico](./images/owm5.png)

Uma **Chave de API** tem esta aparência: `b2c4c36b6bb59c3458d6686b05311dc3`.

Você pode encontrar a **Documentação da API** para a **Previsão atual** [aqui](https://openweathermap.org/current).

Neste caso de uso, você implementará a conexão com o Open Weather Map com base na cidade em que o cliente está, usando a **Solicitação de API interna por nome de cidade**.

![MapaMeteorológico](./images/owm6.png)

Volte para o **Adobe Journey Optimizer**, para o pop-up **External Data Source** vazio.

![Demonstração](./images/emptyds.png)

Como um Nome para a fonte de dados, use `--aepUserLdap--WeatherApi`.

Defina a Descrição como: `Access to the Open Weather Map`.

A URL para a API Abrir Mapa Meteorológico é: `http://api.openweathermap.org/data/2.5/weather?units=metric`.

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

De acordo com a Documentação da API do Tempo, você precisa enviar um parâmetro `q=City`.

![Demonstração](./images/owmapi.png)

Para corresponder à Solicitação de API esperada, configure seu FieldGroup da seguinte maneira:

>[!IMPORTANT]
>
>O nome do grupo de campos deve ser exclusivo, use esta convenção de nomenclatura: `--aepUserLdap--WeatherByCity`

![Demonstração](./images/fg1.png)

Para a Carga de resposta, é necessário colar um exemplo da Resposta que será enviada pela API de Tempo.

Você pode encontrar a Resposta JSON da API esperada na página Documentação da API [aqui](https://openweathermap.org/current), no assunto **JSON**.

![Demonstração](./images/owmapi1.png)

Ou você pode copiar a Resposta JSON daqui:

```json
{
   "coord": {
      "lon": 7.367,
      "lat": 45.133
   },
   "weather": [
      {
         "id": 501,
         "main": "Rain",
         "description": "moderate rain",
         "icon": "10d"
      }
   ],
   "base": "stations",
   "main": {
      "temp": 284.2,
      "feels_like": 282.93,
      "temp_min": 283.06,
      "temp_max": 286.82,
      "pressure": 1021,
      "humidity": 60,
      "sea_level": 1021,
      "grnd_level": 910
   },
   "visibility": 10000,
   "wind": {
      "speed": 4.09,
      "deg": 121,
      "gust": 3.47
   },
   "rain": {
      "1h": 2.73
   },
   "clouds": {
      "all": 83
   },
   "dt": 1726660758,
   "sys": {
      "type": 1,
      "id": 6736,
      "country": "IT",
      "sunrise": 1726636384,
      "sunset": 1726680975
   },
   "timezone": 7200,
   "id": 3165523,
   "name": "Province of Turin",
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

## Próximas etapas

Ir para [3.2.3 Definir uma ação personalizada](./ex3.md){target="_blank"}

Voltar para [Adobe Journey Optimizer: Fontes de dados externas e ações personalizadas](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Voltar para [Todos os módulos](./../../../../overview.md){target="_blank"}
