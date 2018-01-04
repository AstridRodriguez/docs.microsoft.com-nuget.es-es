---
title: Configurar fuentes locales de NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1354a527-d988-43d1-8dcf-6ce46ec5d3d4
description: "Cómo crear una fuente local para los paquetes de NuGet usando carpetas en la red local"
keywords: "Fuente de NuGet, galería de NuGet, fuente local de paquetes"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32217622077ff983abaf00b2e6e5baf3064fff56
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2017
---
# <a name="local-feeds"></a>Fuentes locales

Las fuentes locales de paquetes de NuGet son estructuras jerárquicas de carpetas en la red local (o solo de su equipo) en la que coloca los paquetes. Estas fuentes se pueden usar después como orígenes de paquetes con todas las demás operaciones de NuGet mediante la CLI, la interfaz de usuario del Administrador de paquetes y la consola del Administrador de paquetes.

Para habilitar el origen, agregue el nombre de la ruta de acceso (como `\\myserver\packages`) a la lista de orígenes mediante la [interfaz de usuario del Administrador de paquetes](../tools/package-manager-ui.md#package-sources) o el comando [`nuget sources`](../tools/cli-ref-sources.md).

> [!Note]
> En NuGet 3.3+ se admiten las estructuras de carpetas jerárquicas. Las versiones anteriores de NuGet solo usan una carpeta que contiene paquetes, con los que el rendimiento es mucho menor que la estructura jerárquica.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Inicializar y mantener las carpetas jerárquicas

El árbol jerárquico de carpetas con control de versiones tiene la siguiente estructura general:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

NuGet crea esta estructura automáticamente al usar el comando [`nuget add`](../tools/cli-ref-add.md) para copiar un paquete a la fuente:

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

El comando `nuget add` funciona con un paquete a la vez, lo cual puede ser un problema al configurar una fuente con varios paquetes.

En estos casos, use el comando [`nuget init`](../tools/cli-ref-init.md) para copiar todos los paquetes de una carpeta a la fuente como si ejecutara `nuget add` en cada uno de ellos por separado. Por ejemplo, el siguiente comando copia todos los paquetes de `c:\packages` a un árbol jerárquico en `\\myserver\packages`:

```
nuget init c:\packages \\myserver\packages
```

Al igual que con el comando `add`, `init` crea una carpeta para cada identificador de paquete, cada uno de los cuales contiene una carpeta de número de versión, dentro de la cual se encuentra el paquete adecuado.