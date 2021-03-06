---
ms.assetid: C4DB495D-1F91-40EF-A55C-5CABBF3269A2
description: Windows.Media.Editing 命名空间中的 API 允许你快速开发应用，从而使用户从音频和视频源文件创建媒体合成。
title: 媒体合成和编辑
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 6a0b21ac4c2bc1a2278757cdaa542be39c01f481
ms.sourcegitcommit: 6f32604876ed480e8238c86101366a8d106c7d4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2019
ms.locfileid: "67318256"
---
# <a name="media-compositions-and-editing"></a>媒体合成和编辑



本文向你介绍如何使用 [**Windows.Media.Editing**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing) 命名空间中的 API 来快速开发应用，从而使用户从音频和视频源文件创建媒体合成。 框架的功能包括以编程方式同时追加多个视频剪辑、添加视频和图像覆盖、添加后台音频，以及同时应用音频和视频效果。 创建媒体合成后，可在平面媒体文件中进行呈现以供播放或共享，但合成还可通过磁盘进行序列化和反序列化，从而允许用户加载并修改之前创建的合成。 这一完整功能将在易于使用的 Windows 运行时接口中提供，与低级别 [Microsoft Media Foundation](https://docs.microsoft.com/windows/desktop/medfound/microsoft-media-foundation-sdk) API 相比，它可大大减少执行这些任务所需的代码数量和复杂性。

## <a name="create-a-new-media-composition"></a>创建新的媒体合成

[**MediaComposition**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaComposition) 类是包含组成合成的所有媒体剪辑的容器，用于负责呈现最终合成、将合成加载并保存到光盘，以及提供合成的预览流，以便用户可以在 UI 中查看它。 若要在你的应用中使用 **MediaComposition**，需包括 [**Windows.Media.Editing**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing) 命名空间以及提供你将需要的相关 API 的 [**Windows.Media.Core**](https://docs.microsoft.com/uwp/api/Windows.Media.Core) 命名空间。

[!code-cs[Namespace1](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetNamespace1)]


在你的代码中可通过多个点访问 **MediaComposition** 对象，因此，你通常将声明一个要在其中存储该对象的成员变量。

[!code-cs[DeclareMediaComposition](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetDeclareMediaComposition)]

**MediaComposition** 的构造函数不采用任何参数。

[!code-cs[MediaCompositionConstructor](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetMediaCompositionConstructor)]

## <a name="add-media-clips-to-a-composition"></a>将媒体剪辑添加到合成

媒体合成通常包含一个或多个视频剪辑。 你可以使用 [**FileOpenPicker**](https://docs.microsoft.com/uwp/schemas/appxpackage/appxmanifestschema/element-fileopenpicker) 以允许用户选择某个视频文件。 选择文件后，通过调用 [**MediaClip.CreateFromFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.createfromfileasync) 创建新的 [**MediaClip**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaClip) 对象以包含视频剪辑。 然后，将该剪辑添加到 **MediaComposition** 对象的 [**Clips**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.clips) 列表。

[!code-cs[PickFileAndAddClip](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetPickFileAndAddClip)]

-   媒体剪辑按照它们在 [**Clips**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.clips) 列表中显示的相同顺序显示在 **MediaComposition** 中。

-   **MediaClip** 只能包含在合成中一次。 尝试添加已由合成使用的 **MediaClip** 将导致错误。 若要在合成中多次重复使用视频剪辑，可调用 [**Clone**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.clone) 以创建新的 **MediaClip** 对象，这些对象随后将添加到合成中。

-   通用 Windows 应用没有访问整个文件系统的权限。 [**StorageApplicationPermissions**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageApplicationPermissions) 类的 [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) 属性允许你的应用存储已由用户选择的文件的记录，以便你可以保留访问该文件的权限。 **FutureAccessList** 最多可以包含 1000 个条目，因此你的应用需要管理列表，以确保列表不会饱和。 如果你计划支持加载和修改之前创建的合成，这一点尤其重要。

-   **MediaComposition** 支持采用 MP4 格式的视频剪辑。

-   如果视频文件包含多个嵌入的音轨，通过设置 [**SelectedEmbeddedAudioTrackIndex**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.selectedembeddedaudiotrackindex) 属性可以选择在合成中使用哪个音轨。

-   通过调用 [**CreateFromColor**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.createfromcolor) 并指定该剪辑的颜色和持续时间，创建使用单一颜色填充整个帧的 **MediaClip**。

-   通过调用 [**CreateFromImageFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.createfromimagefileasync) 并指定该剪辑的图像文件和持续时间，从图像文件中创建 **MediaClip**。

-   通过调用 [**CreateFromSurface**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.createfromsurface) 并指定该剪辑的图面和持续时间，从 [**IDirect3DSurface**](https://docs.microsoft.com/uwp/api/Windows.Graphics.DirectX.Direct3D11.IDirect3DSurface) 创建 **MediaClip**。

## <a name="preview-the-composition-in-a-mediaelement"></a>在 MediaElement 中预览合成

若要使用户能够查看媒体合成，将 [**MediaPlayerElement**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement) 添加到定义 UI 的 XAML 文件中。

[!code-xml[MediaElement](./code/MediaEditing/cs/MainPage.xaml#SnippetMediaElement)]

声明类型 [**MediaStreamSource**](https://docs.microsoft.com/uwp/api/Windows.Media.Core.MediaStreamSource) 的成员变量。


[!code-cs[DeclareMediaStreamSource](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetDeclareMediaStreamSource)]

调用 **MediaComposition** 对象的 [**GeneratePreviewMediaStreamSource**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.generatepreviewmediastreamsource) 方法，为合成创建 **MediaStreamSource**。 通过调用工厂方法 [**CreateFromMediaStreamSource**](https://docs.microsoft.com/uwp/api/windows.media.core.mediasource.createfrommediastreamsource) 创建 [**MediaSource**](https://docs.microsoft.com/uwp/api/Windows.Media.Core.MediaSource) 对象，并将其分配给 **MediaPlayerElement** 的 [**Source**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) 属性。 现在，可以在 UI 中查看合成。


[!code-cs[UpdateMediaElementSource](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetUpdateMediaElementSource)]

-   **MediaComposition** 必须包含至少一个媒体剪辑才能调用 [**GeneratePreviewMediaStreamSource**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.generatepreviewmediastreamsource)，否则返回的对象将为 null。

-   **MediaElement** 时间线不会自动更新为反映合成中的更改。 建议同时调用**GeneratePreviewMediaStreamSource**并设置**MediaPlayerElement** **源**属性每次你做的一组更改为组合并想要更新 UI。

建议在用户导航离开页面，以便发布关联的资源时，将 **MediaPlayerElement** 的 **MediaStreamSource** 对象和 [**Source**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.mediaelement.source) 属性设置为 null。

[!code-cs[OnNavigatedFrom](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetOnNavigatedFrom)]

## <a name="render-the-composition-to-a-video-file"></a>将合成呈现到视频文件

若要将媒体合成呈现到平面视频文件，以便在其他设备上进行共享和查看，你将需要使用 [**Windows.Media.Transcoding**](https://docs.microsoft.com/uwp/api/Windows.Media.Transcoding) 命名空间中的 API。 若要在异步操作过程中更新 UI，你还需要使用 [**Windows.UI.Core**](https://docs.microsoft.com/uwp/api/Windows.UI.Core) 命名空间中的 API。

[!code-cs[Namespace2](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetNamespace2)]

允许用户使用 [**FileSavePicker**](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) 选择输出文件后，通过调用 **MediaComposition** 对象的 [**RenderToFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.rendertofileasync) 将合成呈现到选定的文件。 以下示例中的剩余代码只需遵循处理 [**AsyncOperationWithProgress**](https://docs.microsoft.com/previous-versions/br205807(v=vs.85)) 的模式即可。

[!code-cs[RenderCompositionToFile](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetRenderCompositionToFile)]

-   [  **MediaTrimmingPreference**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaTrimmingPreference) 允许你设置转换代码操作的速度与剪裁相邻媒体剪辑的精度的优先级。 **Fast** 导致转换代码的速度更快，但剪裁精度较低，**Precise** 导致转换代码的速度较慢，但剪裁精度较高。

## <a name="trim-a-video-clip"></a>剪裁视频剪辑

通过设置 [**MediaClip**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaClip) 对象的 [**TrimTimeFromStart**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.trimtimefromstart) 属性、[**TrimTimeFromEnd**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.trimtimefromend) 属性或同时设置两者，剪裁合成中视频剪辑的持续时间。

[!code-cs[TrimClipBeforeCurrentPosition](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetTrimClipBeforeCurrentPosition)]

-   你可以使用所需的任何 UI，让用户指定开始和结束剪裁值。 上述示例使用与 **MediaPlayerElement** 关联的 [**MediaPlaybackSession**](https://docs.microsoft.com/uwp/api/Windows.Media.Playback.MediaPlaybackSession) 的 [**Position**](https://docs.microsoft.com/uwp/api/windows.media.playback.mediaplaybacksession.position) 属性，通过检查 [**StartTimeInComposition**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.starttimeincomposition) 和 [**EndTimeInComposition**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.endtimeincomposition)，先确定在合成中的当前位置上播放的是哪个 **MediaClip**。 然后，再次使用 **Position** 和 **StartTimeInComposition** 属性，计算要从剪辑开始处剪裁的时间量。 **FirstOrDefault** 方法是 **System.Linq** 命名空间中的扩展方法，可简化用于从列表中选择项目的代码。
-   通过 **MediaClip** 对象的 [**OriginalDuration**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.originalduration) 属性，你可以在未应用任何剪辑的情况下知道媒体剪辑的持续时间。
-   通过 [**TrimmedDuration**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.trimmedduration) 属性，你可以在应用剪裁后知道媒体剪辑的持续时间。
-   指定一个大于剪辑原始持续时间的剪裁值不会引发错误。 但是，如果合成仅包含单个剪辑，并且通过指定较大的剪裁值将其长度剪裁为零，则对 [**GeneratePreviewMediaStreamSource**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.generatepreviewmediastreamsource) 的后续调用将返回 null，就像合成没有剪辑一样。

## <a name="add-a-background-audio-track-to-a-composition"></a>将后台音轨添加到合成

若要将后台音轨添加到合成，请加载音频文件，然后通过调用工厂方法 [**BackgroundAudioTrack.CreateFromFileAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.backgroundaudiotrack.createfromfileasync) 创建 [**BackgroundAudioTrack**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.BackgroundAudioTrack) 对象。 然后，将 **BackgroundAudioTrack** 添加到合成的 [**BackgroundAudioTracks**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.backgroundaudiotracks) 属性。

[!code-cs[AddBackgroundAudioTrack](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetAddBackgroundAudioTrack)]

-   一个**MediaComposition**支持后台音频轨道采用以下格式：MP3，WAV FLAC

-   后台音轨

-   与视频文件一样，你应用使用 [**StorageApplicationPermissions**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageApplicationPermissions) 类保留对合成中文件的访问权限。

-   与 **MediaClip** 一样，**BackgroundAudioTrack** 只能包含在合成中一次。 尝试添加已由合成使用的 **BackgroundAudioTrack** 将导致错误。 若要在合成中多次重复使用音轨，请调用 [**Clone**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.clone) 以创建新的 **MediaClip** 对象，这些对象随后将添加到合成中。

-   默认情况下，后台音轨在合成的开头开始播放。 如果存在多个后台音轨，将在合成的开头开始播放所有音轨。 若要使后台音轨在其他时间开始播放，请将 [**Delay**](https://docs.microsoft.com/uwp/api/windows.media.editing.backgroundaudiotrack.delay) 属性设置为所需的时间偏移。

## <a name="add-an-overlay-to-a-composition"></a>将覆盖添加到合成

覆盖允许你在合成中各个覆盖顶部堆栈多层视频。 合成可以包含多个覆盖层，每个覆盖层可以包含多个覆盖。 通过将 **MediaClip** 传入其构造函数中来创建 [**MediaOverlay**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaOverlay) 对象。 设置覆盖的位置和不透明度，然后创建新的 [**MediaOverlayLayer**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaOverlayLayer) 并将 **MediaOverlay** 添加到其 [**Overlays**](https://docs.microsoft.com/windows/desktop/api/dxgi1_3/nf-dxgi1_3-idxgioutput2-supportsoverlays) 列表。 最后，将 **MediaOverlayLayer** 添加到合成的 [**OverlayLayers**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.overlaylayers) 列表。

[!code-cs[AddOverlay](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetAddOverlay)]

-   某个层中的覆盖根据其在包含层的 **Overlays** 列表中的顺序，按 z 顺序进行排序。 在该列表内，较高索引呈现在较低索引的顶部。 这对于合成内的覆盖层同样适用。 在合成的 **OverlayLayers** 列表中，具有较高索引的层将呈现在较低索引的顶部。

-   因为覆盖将在各个覆盖顶部堆栈，而不是按顺序播放，因此默认情况下，所有覆盖都将在合成的开头开始播放。 若要使覆盖在其他时间开始播放，请将 [**Delay**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaoverlay.delay) 属性设置为所需的时间偏移。

## <a name="add-effects-to-a-media-clip"></a>将效果添加到媒体剪辑

合成中的每个 **MediaClip** 都具有音频和视频效果列表，可向其中添加多个效果。 效果必须分别实现 [**IAudioEffectDefinition**](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.IAudioEffectDefinition) 和 [**IVideoEffectDefinition**](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.IVideoEffectDefinition)。 以下示例使用当前 **MediaPlayerElement** 位置选择当前查看的 **MediaClip**，然后创建 [**VideoStabilizationEffectDefinition**](https://docs.microsoft.com/uwp/api/Windows.Media.Core.VideoStabilizationEffectDefinition) 的新实例并将其追加到媒体剪辑的 [**VideoEffectDefinitions**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediaclip.videoeffectdefinitions) 列表。

[!code-cs[AddVideoEffect](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetAddVideoEffect)]

## <a name="save-a-composition-to-a-file"></a>将合成保存到文件

媒体合成可序列化为要在以后修改的文件。 选取输出文件，然后调用 [**MediaComposition**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaComposition) 方法 [**SaveAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.saveasync) 以保存合成。

[!code-cs[SaveComposition](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetSaveComposition)]

## <a name="load-a-composition-from-a-file"></a>从文件中加载合成

媒体合成可从文件中进行反序列化，以允许用户查看和修改合成。 选取合成文件，然后调用 [**MediaComposition**](https://docs.microsoft.com/uwp/api/Windows.Media.Editing.MediaComposition) 方法 [**LoadAsync**](https://docs.microsoft.com/uwp/api/windows.media.editing.mediacomposition.loadasync) 以加载合成。

[!code-cs[OpenComposition](./code/MediaEditing/cs/MainPage.xaml.cs#SnippetOpenComposition)]

-   如果合成中的媒体文件不在你的应用可以访问的位置中，并且也不在你的应用的 [**StorageApplicationPermissions**](https://docs.microsoft.com/uwp/api/Windows.Storage.AccessCache.StorageApplicationPermissions) 类的 [**FutureAccessList**](https://docs.microsoft.com/uwp/api/windows.storage.accesscache.storageapplicationpermissions.futureaccesslist) 属性中，当加载该合成时，将引发错误。

 

 




