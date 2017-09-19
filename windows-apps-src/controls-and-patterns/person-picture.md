---
author: mijacobs
description: 
title: "个人图片控件"
template: detail.hbs
label: Parallax View
ms.author: mijacobs
ms.date: 05/19/2017
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
pm-contact: kevjey
design-contact: kimsea
dev-contact: kefodero
doc-status: Published
ms.openlocfilehash: c71fdf3d19c8c8e43666620df53258825c4a8eb1
ms.sourcegitcommit: 10d6736a0827fe813c3c6e8d26d67b20ff110f6c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2017
---
# <a name="person-picture-control"></a>个人图片控件

> [!IMPORTANT]
> 本文介绍的功能尚未发布，在商业发行之前可能发生实质性修改。 Microsoft 不对此处提供的信息作任何明示或默示的担保。

如果用户头像可用，个人图片控件将显示用户头像；否则，将显示该用户的姓名缩写或通用字形。 你可以使用该控件来显示 [Contact 对象](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.Contact)（该对象管理用户的联系信息），你也可以手动提供联系信息，例如显示名称和个人资料图片。  

> **重要 API**：[PersonPicture 类](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.personpicture)、[Contact 类](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.Contact)、[ContactManager 类](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.ContactManager)

![个人图片控件](images/person-picture/person-picture_hero.png)

## <a name="is-this-the-right-control"></a>这是正确的控件吗？

当你想要表示用户及其联系信息时，请使用个人图片。 下面是可能使用该控件的一些示例：
* 显示当前用户
* 显示通讯簿中的联系人
* 显示消息的发送者 
* 显示社交媒体联系人

该图在联系人列表中显示个人图片控件：![个人图片控件](images/person-picture/person-picture-control.png)

## <a name="how-to-use-the-person-picture-control"></a>如何使用个人图片控件

若要创建个人图片，你可以使用 PersonPicture 类。 此示例创建一个 PersonPicture 控件，并手动提供此人的显示名称、个人资料图片和姓名缩写：

```xaml
<Page
    x:Class="App2.ExamplePage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:App2"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <PersonPicture
            DisplayName="Betsy Sherman"
            ProfilePicture="Assets\BetsyShermanProfile.png"
            Initials="BS" />
    </StackPanel>
</Page>
```

## <a name="using-the-person-picture-control-to-display-a-contact-object"></a>使用个人图片控件来显示 Contact 对象

你可以使用用户选取器控件来显示 [Contact](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.Contact) 对象： 

```xaml
<Page
    x:Class="SampleApp.PersonPictureContactExample"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:SampleApp"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <StackPanel Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

        <PersonPicture
            Contact="{x:Bind CurrentContact, Mode=OneWay}" />
            
        <Button Click="LoadContactButton_Click">Load contact</Button>
    </StackPanel>
</Page>
```

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Runtime.InteropServices.WindowsRuntime;
using Windows.Foundation;
using Windows.Foundation.Collections;
using Windows.UI.Xaml;
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Controls.Primitives;
using Windows.UI.Xaml.Data;
using Windows.UI.Xaml.Input;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Navigation;
using Windows.ApplicationModel.Contacts;

namespace SampleApp
{
    public sealed partial class PersonPictureContactExample : Page, System.ComponentModel.INotifyPropertyChanged
    {
        public PersonPictureContactExample()
        {
            this.InitializeComponent();
        }

        private Windows.ApplicationModel.Contacts.Contact _currentContact; 
        public Windows.ApplicationModel.Contacts.Contact CurrentContact
        {
            get => _currentContact;
            set
            {
                _currentContact = value;
                PropertyChanged?.Invoke(this,
                    new System.ComponentModel.PropertyChangedEventArgs(nameof(CurrentContact)));
            }

        }
        public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;

        public static async System.Threading.Tasks.Task<Windows.ApplicationModel.Contacts.Contact> CreateContact()
        {

            var contact = new Windows.ApplicationModel.Contacts.Contact();
            contact.FirstName = "Betsy";
            contact.LastName = "Sherman";

            // Get the app folder where the images are stored.
            var appInstalledFolder = 
                Windows.ApplicationModel.Package.Current.InstalledLocation;
            var assets = await appInstalledFolder.GetFolderAsync("Assets");
            var imageFile = await assets.GetFileAsync("betsy.png");
            contact.SourceDisplayPicture = imageFile;

            return contact;
        }

        private async void LoadContactButton_Click(object sender, RoutedEventArgs e)
        {
            CurrentContact = await CreateContact();
        }
    }
}
```

> [!NOTE]
> 为使代码简单，此示例中创建一个新的 Contact 对象。 在实际应用中，你会让用户选择一个联系人或使用 [ContactManager](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.ContactManager) 查询联系人列表。 有关检索和管理联系人的信息，请参阅[联系人和日历文章](../contacts-and-calendar/index.md)。 

## <a name="determining-which-info-to-display"></a>确定要显示的信息

当你提供 [Contact](https://docs.microsoft.com/en-us/uwp/api/Windows.ApplicationModel.Contacts.Contact) 对象时，个人图片控件将对其进行评估，以确定它可以显示哪些信息。 

如果图像可用，该控件将显示它找到的第一个图像，顺序如下：

1.    LargeDisplayPicture
2.    SmallDisplayPicture
3.    缩略图

通过将 PreferSmallImage 设置为 true 可以更改所选的图像；这将使 SmallDisplayPicture 的优先级比 LargeDisplayPicture 高。

如果没有图像，该控件将显示联系人的姓名或缩写；如果没有任何姓名数据，该控件将显示联系人数据，如电子邮件地址或电话号码。 

## <a name="related-articles"></a>相关文章

* [联系人和日历](../contacts-and-calendar/index.md)
* [联系人卡片示例](http://go.microsoft.com/fwlink/p/?LinkId=624040)



