---
title: NuGet CLI comprobar comando | Documentos de Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: Comprobar la referencia para el nuget.exe comando
keywords: NuGet comprobar la referencia, compruebe el comando
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 096c79670267d9b602dd6ad30640e832441c31c5
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="58c09-104">Compruebe el comando (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="58c09-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="58c09-105">**Se aplica a:** paquete consumo &bullet; **versiones admitidas:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="58c09-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="58c09-106">Comprueba un paquete.</span><span class="sxs-lookup"><span data-stu-id="58c09-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="58c09-107">Uso</span><span class="sxs-lookup"><span data-stu-id="58c09-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="58c09-108">donde `<package(s)>` es uno o más `.nupkg` archivos.</span><span class="sxs-lookup"><span data-stu-id="58c09-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="58c09-109">Opciones</span><span class="sxs-lookup"><span data-stu-id="58c09-109">Options</span></span>

| <span data-ttu-id="58c09-110">Opción</span><span class="sxs-lookup"><span data-stu-id="58c09-110">Option</span></span> | <span data-ttu-id="58c09-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="58c09-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58c09-112">Todas</span><span class="sxs-lookup"><span data-stu-id="58c09-112">All</span></span> | <span data-ttu-id="58c09-113">Especifica que se deben realizar todas las comprobaciones de posibles en los paquetes.</span><span class="sxs-lookup"><span data-stu-id="58c09-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="58c09-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="58c09-114">CertificateFingerprint</span></span> | <span data-ttu-id="58c09-115">Especifica uno o más SHA-256 certificado las huellas digitales de certificados (s) de los paquetes con firma deben estar firmados con.</span><span class="sxs-lookup"><span data-stu-id="58c09-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="58c09-116">Una huella digital del certificado SHA-256 es un hash SHA-256 del certificado.</span><span class="sxs-lookup"><span data-stu-id="58c09-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="58c09-117">Varias entradas deben ser separado de punto y coma.</span><span class="sxs-lookup"><span data-stu-id="58c09-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="58c09-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="58c09-118">ConfigFile</span></span> | <span data-ttu-id="58c09-119">El archivo de configuración de NuGet para aplicar.</span><span class="sxs-lookup"><span data-stu-id="58c09-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="58c09-120">Si no se especifica, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac o Linux) se utiliza.</span><span class="sxs-lookup"><span data-stu-id="58c09-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="58c09-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="58c09-121">ForceEnglishOutput</span></span> | <span data-ttu-id="58c09-122">Fuerza nuget.exe ejecutándose con una referencia cultural invariable, basados en el inglés.</span><span class="sxs-lookup"><span data-stu-id="58c09-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="58c09-123">Ayuda</span><span class="sxs-lookup"><span data-stu-id="58c09-123">Help</span></span> | <span data-ttu-id="58c09-124">Muestra información de ayuda para el comando.</span><span class="sxs-lookup"><span data-stu-id="58c09-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="58c09-125">No interactivo</span><span class="sxs-lookup"><span data-stu-id="58c09-125">NonInteractive</span></span> | <span data-ttu-id="58c09-126">Suprime los mensajes para la entrada de usuario o confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="58c09-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="58c09-127">Prototipos</span><span class="sxs-lookup"><span data-stu-id="58c09-127">Signatures</span></span> | <span data-ttu-id="58c09-128">Especifica que se debe realizar la comprobación de firmas de paquete.</span><span class="sxs-lookup"><span data-stu-id="58c09-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="58c09-129">Nivel de detalle</span><span class="sxs-lookup"><span data-stu-id="58c09-129">Verbosity</span></span> | <span data-ttu-id="58c09-130">Especifica la cantidad de detalle que se muestra en la salida: *normal*, *quiet*, *detallada*.</span><span class="sxs-lookup"><span data-stu-id="58c09-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="58c09-131">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="58c09-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```