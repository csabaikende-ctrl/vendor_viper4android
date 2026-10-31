# vendor_viper4android

ViPER4Android RE for ROM integration (legacy / non-AIDL audio effect HAL).

| Component | Upstream | Version | License | Installed to |
|---|---|---|---|---|
| App (`com.llsl.viper4android`, Material 3) | [likelikeslike/ViPER4Android](https://github.com/likelikeslike/ViPER4Android/tree/2.1.1) | 2.1.1 | GPL-3.0 | `/product/priv-app/ViPER4Android` |
| Driver `libv4a_re.so` | [likelikeslike/ViPERFX_RE](https://github.com/likelikeslike/ViPERFX_RE/tree/v2.1.1) | v2.1.1 | GPL-2.0 | `/vendor/lib{,64}/soundfx` |

The files under `prebuilt/` are the unmodified upstream release artifacts
(`ViPER4Android-2.1.1.apk` and `common/files/libv4a_re_*.so` from
`ViPER4Android-RE-v2.1.1.zip`). Source code for both is available at the links above.

```
b60a8e38c4abf00b5e3f0d4802732bf1dc8679047cc9471fb36bf74a9c572cba  prebuilt/app/ViPER4Android.apk
79d058309902ec3a7ac96e225cf052aefe950d8a904a7f405e633916284cd31b  prebuilt/lib/arm64/libv4a_re.so
6f57536c87445b2648ebfe67efd0c67a48ee6b97e78fdd44b04a3f9ac43237b7  prebuilt/lib/arm/libv4a_re.so
```

## Usage

```make
$(call inherit-product, vendor/viper4android/config.mk)
```

The device must also register the effect in its `audio_effects.xml`:

```xml
<library name="v4a_re" path="libv4a_re.so"/>
<effect name="v4a_standard_re" library="v4a_re" uuid="90380da3-8536-4744-a6a3-5731970e640f"/>
```

Only for devices whose audio effect HAL is HIDL (`android.hardware.audio.effect@x.0`).
Devices with the AIDL effect HAL need the AIDL driver instead.
