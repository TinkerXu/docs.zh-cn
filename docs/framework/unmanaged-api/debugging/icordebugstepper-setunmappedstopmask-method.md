---
title: ICorDebugStepper::SetUnmappedStopMask 方法
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetUnmappedStopMask
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetUnmappedStopMask
helpviewer_keywords:
- ICorDebugStepper::SetUnmappedStopMask method [.NET Framework debugging]
- SetUnmappedStopMask method [.NET Framework debugging]
ms.assetid: b1211981-e90c-4e05-8def-fa18d85ad9ab
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dc4e51ec60c7526f36bbe4909bec91a527e0862c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33419905"
---
# <a name="icordebugsteppersetunmappedstopmask-method"></a>ICorDebugStepper::SetUnmappedStopMask 方法
设置一个值，指定的顺序，则执行将暂停的非托管代码的类型。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetUnmappedStopMask (  
    [in] CorDebugUnmappedStop   mask  
);  
```  
  
#### <a name="parameters"></a>参数  
 `mask`  
 [in]CorDebugUnmappedStop 枚举，指定的顺序，则调试器将暂停执行的非托管代码的类型的值。  
  
 默认值为 STOP_OTHER_UNMAPPED。 STOP_UNMANAGED 的值才有效，且互操作调试。  
  
## <a name="remarks"></a>备注  
 当调试器发现没有相应 Microsoft 中间语言 (MSIL) 到映射中实时 (JIT) 编译时，它可以暂停执行，如果已设置标志，指定该类型的非托管代码;否则，继续单步以透明方式执行。  
  
 如果调试器未使用分档器输入的方法，然后它将不一定逐过程执行未映射代码。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
