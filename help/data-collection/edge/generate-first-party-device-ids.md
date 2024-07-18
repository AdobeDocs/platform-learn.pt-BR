---
title: Gerar IDs de dispositivo primário
description: Saiba como gerar IDs de dispositivos primários
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Gerar IDs de dispositivo primário

Tradicionalmente, os aplicativos do Adobe Experience Cloud geram cookies para armazenar ids de dispositivos usando diferentes tecnologias, incluindo:

1. Cookies de terceiros
1. Cookies primários definidos por um servidor Adobe usando a configuração CNAME de um nome de domínio
1. Cookies próprios definidos pelo JavaScript

Alterações recentes no navegador restringem a duração desses tipos de cookies. Os cookies primários são mais eficazes quando são definidos usando um servidor de propriedade do cliente usando um registro DNS A/AAAA em vez de um CNAME DNS. A funcionalidade de ID de dispositivo próprio (FPID) permite que os clientes que implementam o SDK da Web da Adobe Experience Platform usem IDs de dispositivo em cookies de servidores que usam registros DNS A/AAAA. Essas IDs podem ser enviadas para o Adobe e usadas como seeds para gerar IDs de Experience Cloud (ECIDs), que permanecem como o identificador principal nos aplicativos da Adobe Experience Cloud.

Este é um exemplo rápido de como a funcionalidade funciona:

![IDs de dispositivo primário (FPIDs) e IDs de Experience Cloud (ECIDs)](../assets/kt-9728.png)

1. O navegador de um usuário final solicita uma página da Web do servidor Web de um cliente ou CDN.
1. O cliente gera uma ID de dispositivo (FPID) em seu servidor da Web ou CDN (o servidor da Web deve estar vinculado ao registro DNS A/AAAA do nome do domínio).
1. O cliente define um cookie próprio para armazenar o FPID no navegador do usuário final.
1. A implementação do SDK da Web da Adobe Experience Platform do cliente faz uma solicitação ao Edge Network da plataforma, incluindo o FPID no mapa de identidade.
1. O Experience Platform Edge Network recebe o FPID e o usa para gerar um Experience Cloud ID (ECID).
1. A resposta do SDK da Web da Platform envia a ECID de volta para o navegador do usuário final.
1. Se o `idMigrationEnabled=true`, o SDK da Web da Platform usará o JavaScript para armazenar a ECID como o cookie `AMCV_` no navegador do usuário final.
1. Caso o cookie `AMCV_` expire, o processo se repetirá. Desde que a mesma ID de dispositivo próprio esteja disponível, um novo cookie `AMCV_` é criado com o mesmo valor de ECID de antes.

>[!NOTE]
>
>O `idMigrationEnabled` não precisa ser configurado como `true` para usar FPID. No entanto, com `idMigrationEnabled=false` você pode não ver um cookie `AMCV_` e precisará procurar o valor ECID na resposta da rede.


Para este tutorial, um exemplo específico usando a linguagem de script PHP é usado para mostrar como:

* Gerar um UUIDv4
* Gravar o valor UUIDv4 em um cookie
* Incluir o valor do cookie no mapa de identidade
* Validar a geração da ECID

Outra documentação relacionada às IDs de dispositivos primários pode ser encontrada na documentação do produto.

## Gerar um UUIDv4

O PHP não tem uma biblioteca nativa para geração UUID, então estes exemplos de código são mais extensos do que o que seria necessário se outra linguagem de programação fosse usada. O PHP foi escolhido para este exemplo porque é uma linguagem do lado do servidor amplamente suportada.


Quando a seguinte função é chamada, ela gera um UUID aleatório versão 4:

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## Gravar o valor UUIDv4 em um cookie

O código a seguir faz uma solicitação à função acima para gerar uma UUID. Em seguida, ele define os sinalizadores de cookie decididos pela sua organização. Se um cookie já tiver sido gerado, a expiração será estendida.

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>O cookie que contém a ID de dispositivo primário pode ter qualquer nome.

## Incluir o valor do cookie no Mapa de identidade

O passo final é usar o PHP para ecoar o valor do cookie no Mapa de identidade.


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>O símbolo de namespace de identidade usado no mapa de identidade deve ser chamado `FPID`.
>
> `FPID` é um namespace de identidade reservado que não está visível nas listas de interface de namespaces de identidade.


## Validar geração de ECID

Valide a implementação confirmando que a mesma ECID é gerada a partir da ID de dispositivo primário:

1. Gere um cookie FPID.
1. Envie uma solicitação para o Platform Edge Network usando o SDK da Web da plataforma.
1. Um cookie com o formato `AMCV_<IMSORGID@AdobeOrg>` é gerado. Esse cookie contém a ECID.
1. Anote o valor do cookie gerado e exclua todos os cookies do site, exceto o cookie `FPID`.
1. Envie outra solicitação para o Platform Edge Network.
1. Confirme se o valor no cookie `AMCV_<IMSORGID@AdobeOrg>` é igual ao valor `ECID` do cookie `AMCV_` que foi excluído. Se o valor do cookie for o mesmo para um determinado FPID, o processo de propagação da ECID foi bem-sucedido.

Para obter mais informações sobre este recurso, consulte [a documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
