# zmckit-library

`zmckit-library` uygulamalarınıza kamera işlevlerini entegre etmeyi kolaylaştıran bir React Native kütüphanesidir. Bu kütüphane, Snap Camera ile sorunsuz şekilde çalışarak görüntü yakalama ve lens değiştirme işlemlerini yönetir.

## Installation

`zmckit-library` kütüphanesini Yarn veya npm kullanarak kurabilirsiniz:

```sh
# Yarn ile
yarn add https://github.com/ziylanmedya/ZMCameraKit-ReactNative.git

# npm ile
npm add https://github.com/ziylanmedya/ZMCameraKit-ReactNative.git
```

## İzinler

### Android

`AndroidManifest.xml` dosyanıza aşağıdaki izinleri ekleyin::

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera" />
```

### iOS

`Info.plist` dosyanıza aşağıdaki anahtarı ekleyin:

```xml
<key>NSCameraUsageDescription</key>
<string>Görüntü yakalamak için kameranıza erişim izni gerekmektedir.</string>
```

## Kullanım

### Bileşenleri İçe Aktarma

`react-native-zmckit-library` kütüphanesinden gerekli bileşenleri içe aktardığınızdan emin olun:

```tsx
import {
  SingleProductView,
  GroupProductView,
} from "react-native-zmckit-library";
```

### `SingleProductView` Kullanımı

```tsx
<SingleProductView
  apiToken="YOUR_API_TOKEN"
  lensId="YOUR_LENS_ID"
  groupId="YOUR_GROUP_ID"
  onImageCaptured={(imageUri) => console.log("Image captured:", imageUri)}
/>
```

#### `SingleProductView` Özellikleri

| Özellik           | Tip      | Gerekli  | Default | Açıklama                      |
| ----------------- | -------- | -------- | ------- | ----------------------------- |
| `apiToken`        | string   | Yes      | -       | API kimlik doğrulama token’ı  |
| `lensId`          | string   | Yes      | -       | Tekil ürün için lens ID       |
| `groupId`         | string   | Yes      | -       | Tekil ürün için grup ID       |
| `showFrontCamera` | boolean  | No       | `false` | Ön kamerayı etkinleştir       |
| `showPreview`     | boolean  | No       | `true`  | Önizlemeyi göster             |
| `onImageCaptured` | function | Yes      | -       | Foto çekildiğinde çağrılır    |

### Using `GroupProductView`

```tsx
<GroupProductView
  apiToken="YOUR_API_TOKEN"
  groupId="YOUR_GROUP_ID"
  onImageCaptured={(imageUri) => console.log("Image captured:", imageUri)}
  onLensChange={(lensId) => console.log("Lens changed to:", lensId)}
/>
```

#### `GroupProductView` Kullanımı

 Özellik           | Tip      | Gerekli  | Default | Açıklama                       |
| ----------------- | -------- | -------- | ------- | ----------------------------- |
| `apiToken`        | string   | Yes      | -       | API kimlik doğrulama token’ı  |
| `groupId`         | string   | Yes      | -       | Çoklu ürün için grup ID       |
| `showFrontCamera` | boolean  | No       | `false` | Ön kamerayı etkinleştir       |
| `showPreview`     | boolean  | No       | `true`  | Önizlemeyi göster             |
| `onImageCaptured` | function | Yes      | -       | Foto çekildiğinde çağrılır    |
| `onLensChange`    | function | No       | -       | Lens değiştiğinde çağrılır    |

## Ek Kaynaklar ve Özellikler

### Android Paylaşım Özelliği
Paylaşım özelliği önizleme aşamasındadır. Android'de etkinleştirmek için `AndroidManifest.xml` dosyanıza aşağıdaki yapılandırmayı ekleyin:

```xml
<provider
    android:name="androidx.core.content.FileProvider"
    android:authorities="${applicationId}.provider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths" />
</provider>
```

Ve `res/xml/` klasörünün altına `file_paths.xml` dosyasını ekleyin:

```xml
<?xml version="1.0" encoding="utf-8"?>
<paths>
    <cache-path name="cache" path="." />
</paths>
```

