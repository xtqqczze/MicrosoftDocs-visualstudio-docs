---
title: Update existing project or item templates
description: Use the Visual Studio Export Template Wizard or a manual process to update existing project or item templates.
ms.date: 04/14/2025
ms.topic: how-to
helpviewer_keywords:
- item templates, updating
- Visual Studio templates, updating
- project templates, updating
- updating templates [Visual Studio]
author: ghogen
ms.author: ghogen
manager: mijacobs
ms.subservice: general-ide

#customer intent: As a developer, I want to learn how to edit project and item templates in Visual Studio, so I can easily keep my templates up to date.
---

# Update existing templates

After you create a Visual Studio project or item template by compressing the template files into a *.zip* file, you might want to modify the template. This article explains how to modify an existing template by using the **Export Template Wizard** or by manually changing the files in the template.

## Use the Export Template Wizard

You can use the Visual Studio **Export Template Wizard** to update an existing template.

1. Choose **File** > **New** > **Project** from the menu bar.

1. Select the project template you want. If you want to update an existing project template, select that template.

1. Follow the steps to create the new project.

1. To change the project template, modify the project in Visual Studio. For example, change the output type or add a new file to the project.

1. To change an item template, select **Project** > **Add New Item**, and add the item template from the **Add New Item** dialog box. Make any changes you want in the item.

1. On the **Project** menu, choose **Export Template**. The **Export Template Wizard** opens.

1. On the **Template Type** page, select either **Project Template** or **Item Template**, depending on which type you want to export.

1. Follow the prompts in the wizard to export the template as a *.zip* file.

1. If you select the option to **Automatically import the template into Visual Studio**, the wizard places the *.zip* file in the *\\ProjectTemplates* or *\\ItemTemplates* folder at *%USERPROFILE%\Documents\Visual Studio \<version\>\Templates* to make it available for future projects. If you don't select this option, paste the *.zip* file in the user template location manually.

1. Delete the old template *.zip* file if necessary.

## Manually update an existing template

You can update an existing template without using the **Export Template Wizard** by manually modifying the files in the template *.zip* file.

1. Locate the *.zip* file that contains the template. User templates are located in the *\\ProjectTemplates* or *\\ItemTemplates* folder at *%USERPROFILE%\Documents\Visual Studio \<version\>\Templates*.

1. Extract the *.zip* file.

1. Modify the current template files, or delete or add new files to a project template.

1. Open, modify, and save the *.vstemplate* XML file to handle updated behavior or new files.

   For more information about the *.vstemplate* schema, see the [Visual Studio template schema reference](../extensibility/visual-studio-template-schema-reference.md). For more information about what you can parameterize in the source files, see [Template parameters](template-parameters.md).

1. In Windows Explorer, select the files for your template, including the *.vstemplate* file. Right-click the selection and select **Compress to** > **ZIP File**.

1. Copy the resulting *.zip* file and paste it in the same directory as the old *.zip* file.

1. Delete the extracted template files, and delete the old template *.zip* file if necessary.

## Related content

- [Project and item templates](creating-project-and-item-templates.md)
- [Customize templates](customizing-project-and-item-templates.md)
- [Template parameters](template-parameters.md)
- [Visual Studio template schema reference](../extensibility/visual-studio-template-schema-reference.md)
