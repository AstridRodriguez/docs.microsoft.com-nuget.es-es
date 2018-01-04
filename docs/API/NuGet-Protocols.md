---
title: Protocolos de NuGet.org | Documentos de Microsoft
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Los protocolos de nuget.org en constante evolución para interactuar con los clientes de NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a>Protocolos de NuGet.org

Para interactuar con nuget.org, los clientes deben seguir ciertas protocolos. Dado que estos protocolos mantengan evolucionando, los clientes deben identificar la versión de protocolo que se usan cuando se llama a nuget.org específico API. Esto permite nuget.org introducir cambios de una manera poco problemático para los clientes anteriores.

> [!Note]
> Las API documentadas en esta página son específicas de nuget.org y no hay ninguna expectativa para otras implementaciones del servidor de NuGet introducir estas API. 

Para obtener información acerca de la API de NuGet implementan ampliamente en el ecosistema de NuGet, consulte el [Introducción a la API](overview.md).

Este tema enumeran varios protocolos como y cuando descubren a su existencia.

## <a name="nuget-protocol-version-410"></a>Versión de protocolo de NuGet 4.1.0

La 4.1.0 protocolo especifica el uso de claves de comprobar el ámbito para interactuar con los servicios que no sea nuget.org, para validar un paquete con una cuenta de nuget.org. Tenga en cuenta que el `4.1.0` versión número es una cadena opaca, pero no ocurre para que coincida con la primera versión del cliente NuGet oficial que admiten este protocolo.

La validación garantiza que las claves de API creados por el usuario sólo se utilizan con nuget.org, y que otros comprobación o validación de un servicio de terceros se controla mediante una clave de comprobar el ámbito de un solo uso. Estas claves de comprobar el ámbito pueden usarse para validar que el paquete pertenece a un usuario determinado (cuenta) en nuget.org.

### <a name="client-requirement"></a>Requisitos de cliente

Los clientes tienen que pasar el encabezado siguiente cuando realicen llamadas de API a **inserción** paquetes en nuget.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Tenga en cuenta que la preexistente `X-NuGet-Client-Version` encabezado tiene el mismo propósito, pero está en desuso y ya no debe usarse.

El **inserción** protocolo en sí se describe en la documentación de la [ `PackagePublish` recursos](package-publish-resource.md).

Si un cliente interactúa con servicios externos y necesidades para validar si un paquete pertenece a un usuario determinado (cuenta), debe usar el siguiente protocolo y utilizar las teclas de comprobar el ámbito y no las claves de API de nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API para solicitar una clave de comprobar el ámbito

Esta API se utiliza para obtener una clave de comprobar el ámbito de un autor nuget.org validar un paquete de la propiedad por él mismo.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parámetros de solicitud

Name           | En     | Tipo   | Obligatorio | Notas
-------------- | ------ | ------ | -------- | -----
Id.             | Dirección URL    | string | sí      | El identidier de paquete para el que se solicita la clave de ámbito Compruebe
VERSION        | Dirección URL    | string | No       | La versión del paquete
X-NuGet-ApiKey | Header | string | sí      | Por ejemplo, `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Respuesta

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API para comprobar la clave de ámbito Compruebe

Esta API se utiliza para validar una clave de comprobar el ámbito de paquete propiedad por el autor de nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parámetros de solicitud

Name           | En     | Tipo   | Obligatorio | Notas
-------------  | ------ | ------ | -------- | -----
Id.             | Dirección URL    | string | sí      | El identificador de paquete para el que se solicita la clave de ámbito Compruebe
VERSION        | Dirección URL    | string | No       | La versión del paquete
X-NuGet-ApiKey | Header | string | sí      | Por ejemplo, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Esta clave de API de ámbito Compruebe expira en un momento del día o use por primera vez, lo que ocurra primero.

#### <a name="response"></a>Respuesta

Código de estado | Significado
----------- | -------
200         | La clave de API es válida
403         | La clave de API no es válido o no autorizados para insertar en el paquete
404         | El paquete al que hace referencia `ID` y `VERSION` (opcional) no existe