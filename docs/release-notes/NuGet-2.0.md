---
title: Notas de la versión 2.0 de NuGet
description: Notas de la versión 2.0 de NuGet incluidos problemas conocidos, correcciones de errores, características agregadas y dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547580"
---
# <a name="nuget-20-release-notes"></a>Notas de la versión 2.0 de NuGet

[Notas de la versión de NuGet 1.8](../release-notes/nuget-1.8.md) | [notas de la versión 2.1 de NuGet](../release-notes/nuget-2.1.md)

NuGet 2.0 se publicó en 19 de junio de 2012.

## <a name="known-installation-issue"></a>Problema de instalación conocidos
Si está ejecutando VS 2010 SP1, es posible que experimenta un error de instalación al intentar actualizar NuGet si tiene instalada una versión anterior.

La solución consiste en desinstalar NuGet y, a continuación, vuelva a instalarlo desde la Galería de extensiones de VS.  Consulte [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) para obtener más información, o [vaya directamente a la revisión de VS](http://bit.ly/vsixcertfix).

Nota: Si Visual Studio no podrá desinstalar la extensión (está deshabilitado el botón desinstalar), a continuación, es posible que deben reiniciar Visual Studio con la opción "Ejecutar como administrador".

## <a name="package-restore-consent-is-now-active"></a>Ahora está activo el consentimiento de restauración del paquete

Como se describe en este [envíelas consentimiento de restauración del paquete](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 ahora requerirá que se dé su consentimiento para habilitar la restauración de paquetes que se conecte y descargar los paquetes. Asegúrese de que haya proporcionado consentimiento a través de la variable de entorno EnableNuGetPackageRestore o el cuadro de diálogo de configuración de administrador de paquetes.

## <a name="group-dependencies-by-target-frameworks"></a>Dependencias de grupo por marcos de destino

A partir de la versión 2.0, pueden variar las dependencias de paquete que se basa en el perfil de plataforma del proyecto de destino. Esto se logra mediante un controlador actualizado `.nuspec` esquema. El `<dependencies>` elemento puede contener ahora un conjunto de `<group>` elementos. Cada grupo contiene cero o más `<dependency>` elementos y un `targetFramework` atributo. Todas las dependencias dentro de un grupo se instalan conjuntamente si la plataforma de destino es compatible con el perfil de plataforma del proyecto de destino. Por ejemplo:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Tenga en cuenta que un grupo puede contener **cero** dependencias. En el ejemplo anterior, si el paquete está instalado en un proyecto cuyo destino sea Silverlight 3.0 o posterior, no se instalará dependencias. Si el paquete está instalado en un proyecto que tiene como destino .NET 4.0 o posterior, se instalará dos dependencias, jQuery y WebActivar.  Si el paquete está instalado en un proyecto que tiene como destino una versión anterior de estos marcos de 2 trabajo, o cualquier otro marco, se instalará RouteMagic 1.1.0. No hay ningún herencia entre grupos. Si .NET framework de destino del proyecto coincide con el `targetFramework` se instalará el atributo de un grupo, solo las dependencias dentro de ese grupo.

Un paquete puede especificar las dependencias del paquete de cualquiera de los dos formatos: el formato anterior de una lista plana de `<dependency>` elementos o grupos. Si el `<group>` se usa el formato, el paquete no se puede instalar en versiones de NuGet anteriores a 2.0.

Tenga en cuenta que no se permite mezclar los dos formatos. Por ejemplo, el siguiente fragmento es **válido** y se rechazarán con NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Agrupar los archivos de contenido y scripts de PowerShell por .NET framework de destino

Además de las referencias de ensamblado, los archivos de contenido y scripts de PowerShell también se pueden agrupar por .NET framework de destino. La misma estructura de carpetas se encuentra en la `lib` ahora se puede aplicar la carpeta para especificar la plataforma de destino de la misma manera para el `content` y `tools` carpetas. Por ejemplo:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Tenga en cuenta**: porque `init.ps1` se ejecuta en el nivel de solución y es dependiente en cualquier proyecto individual, se debe colocar directamente bajo el `tools` carpeta. Si se coloca dentro de una carpeta específica del marco, se omitirá.

Además, una nueva característica de NuGet 2.0 es que puede ser una carpeta de plataforma *vacía*, en cuyo caso, NuGet agregará no agregue referencias de ensamblado, los archivos de contenido o ejecutar scripts de PowerShell para la versión del marco de trabajo concreto. En el ejemplo anterior, la carpeta `content\net40` está vacío.

## <a name="improved-tab-completion-performance"></a>Rendimiento de la finalización de tabulación mejorada
La característica de finalización en la consola de administrador de paquetes de NuGet se actualizó para mejorar significativamente el rendimiento. Será mucho menos retraso desde el momento en que se presiona la tecla tab hasta que aparezca la lista desplegable de sugerencias.

## <a name="bug-fixes"></a>Correcciones de errores
NuGet 2.0 incluye numerosas correcciones de errores con un énfasis en el rendimiento y el consentimiento de restauración del paquete.
Para obtener una lista completa de trabajo elementos corregidos en NuGet 2.0, por favor, ver el [Issue Tracker para esta versión de NuGet](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
