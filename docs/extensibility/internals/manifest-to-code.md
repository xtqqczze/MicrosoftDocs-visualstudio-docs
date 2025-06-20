---
title: Manifest to Code
description: Learn how to use the Manifest from Code tool that takes an .imagemanifest file for use with the Visual Studio Image Service.
ms.date: 11/04/2016
ms.topic: reference
author: tinaschrepfer
ms.author: tinali
manager: mijacobs
ms.subservice: extensibility-integration
---
# Manifest to Code

The Manifest to Code tool is a console application that takes an .imagemanifest file for the Visual Studio Image Service and generates a wrapper file or files for referencing the image manifest's values in C++, C#, VB, or .vsct files for Visual Studio extensions. This tool generates wrapper files that can be used for requesting images from the Visual Studio Image Service directly, or for passing the manifest values through APIs if the code does not handle any of its own UI and rendering.

## How to use the tool
 **Syntax**

 ManifestToCode /manifest:\<Image Manifest file> /language:\<Code Language> \<Optional Args>

 **Arguments**

|**Switch name**|**Notes**|**Required or Optional**|
|-|-|-|
|/manifest|The path to the image manifest to use to create or update the code wrapper.|Required|
|/language|The language in which to generate the code wrapper.<br /><br /> Valid values: CPP, C++, CS, CSharp, C#, VB, or VSCT The values are case-insensitive.<br /><br /> For the VSCT language option, the /monikerClass, /classAccess, and /namespace options are ignored.|Required|
|/imageIdClass|The name of the imageIdClass and the associated file created by the tool. For the C++ language option, only .h files are generated.<br /><br /> Default: \<Manifest Path>\MyImageIds.\<Lang Ext>|Optional|
|/monikerClass|The name of the monikerClass and the associated file created by the tool. For the C++ language option, only .h files are generated. This is ignored for the VSCT language.<br /><br /> Default: \<Manifest Path>\MyMonikers.\<Lang Ext>|Optional|
|/classAccess|The access modifier for the imageIdClass and the monikerClass. Make sure the access modifier is valid for the given language. This is ignored for the VSCT language option.<br /><br /> Default: Public|Optional|
|/namespace|The namespace defined in the code wrapper. This is ignored for the VSCT language option. Either '.' or '::' are valid namespace separators, regardless of the chosen language option.<br /><br /> Default: MyImages|Optional|
|/noLogo|Setting this flag stops product and copyright information from printing.|Optional|
|/?|Print out Help information.|Optional|
|/help|Print out Help information.|Optional|

 **Examples**

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:CSharp

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:C++                /namespace:My::Namespace                /imageIdClass:MyImageIds                /monikerClass:MyMonikers                /classAccess:friend

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:VSCT                /imageIdClass:MyImageIds

## Notes

- We recommend that you use this tool with image manifests that were generated by the Manifest from Resources tool.

- The tool only looks at symbol entries to generate the code wrappers. If an image manifest contains no symbols, then the generated code wrappers will be empty. If there is an image or set of images in the image manifest that do not use symbols, then they will be excluded from the code wrapper.

## Sample output
 **C# wrappers**

 A pair of simple image ID and image moniker classes for C# will be similar to the below code:

```csharp
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

using System;

namespace MyImages
{
    public static class MyImageIds
    {
        public static readonly Guid AssetsGuid = new Guid("{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}");

        public const int MyImage1 = 0;
        public const int MyImage2 = 1;
    }
}
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

using Microsoft.VisualStudio.Imaging.Interop;

namespace MyImages
{
    public static class MyMonikers
    {
        public static ImageMoniker MyImage1 { get { return new ImageMoniker { Guid = MyImageIds.AssetsGuid, Id = MyImageIds.MyImage1 }; } }
        public static ImageMoniker MyImage2 { get { return new ImageMoniker { Guid = MyImageIds.AssetsGuid, Id = MyImageIds.MyImage2 }; } }
    }
}
```

 **C++ wrappers**

 A pair of simple image ID and image moniker classes for C++ will be similar to the below code:

```cpp
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

#pragma once

#include <guiddef.h>

namespace MyImages {

class MyImageIds {
public:

    static const GUID AssetsGuid;

    static const int MyImage1 = 0;
    static const int MyImage2 = 1;

};

__declspec(selectany) const GUID MyImageIds::AssetsGuid = {0x442d8739,0xefde,0x46a4,{0x8f,0x29,0xe3,0xa1,0xe5,0xe7,0xf8,0xb4}};

}
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

#pragma once

#include "ImageParameters140.h"
#include "MyImageIds.h"

namespace MyImages {

class MyMonikers {
public:

    static const ImageMoniker MyImage1;
    static const ImageMoniker MyImage2;

};

__declspec(selectany) const ImageMoniker MyMonikers::MyImage1 = { MyImageIds::AssetsGuid, MyImageIds::MyImage1 };
__declspec(selectany) const ImageMoniker MyMonikers::MyImage2 = { MyImageIds::AssetsGuid, MyImageIds::MyImage2 };

}
```

 **Visual Basic wrappers**

 A pair of simple image ID and image moniker classes for Visual Basic will be similar to the below code:

```vb
' -----------------------------------------------------------------------------
'  <auto-generated>
'      This code was generated by the ManifestToCode tool.
'      Tool Version: 14.0.15198
'  </auto-generated>
' -----------------------------------------------------------------------------

Imports System

Namespace MyImages

    Public Module MyImageIds

        Public Shared ReadOnly AssetsGuid As Guid = New Guid("{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}")

        Public Const MyImage1 As Integer = 0
        Public Const MyImage2 As Integer = 1

    End Module

End Namespace
' -----------------------------------------------------------------------------
'  <auto-generated>
'      This code was generated by the ManifestToCode tool.
'      Tool Version: 14.0.15198
'  </auto-generated>
' -----------------------------------------------------------------------------

Imports Microsoft.VisualStudio.Imaging.Interop

Namespace MyImages

    Public Module MyMonikers

        Public Readonly Property MyImage1
            Get
                Return New ImageMoniker With {.Guid = MyImageIds.AssetsGuid, .Id = MyImageIds.MyImage1}
            End Get
        End Property

        Public Readonly Property MyImage2
            Get
                Return New ImageMoniker With {.Guid = MyImageIds.AssetsGuid, .Id = MyImageIds.MyImage2}
            End Get
        End Property

    End Module

End Namespace
```

 **VSCT wrapper**

 A set of image IDs for a .vsct file will be similar to this:

```xml
<?xml version='1.0' encoding='utf-8'?>
<!--
- [auto-generated]
     This code was generated by the ManifestToCode tool.
     Tool Version: 14.0.15198
- [/auto-generated]
-->
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
  <Symbols>
    <GuidSymbol name="AssetsGuid" value="{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}">
      <IDSymbol name="MyImage1" value="0" />
      <IDSymbol name="MyImage2" value="1" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```
