# Minimal TWRP Extended

**Init minimal TWRP**

```bash
repo init --depth=1 -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-8.1
```

**Add the local manifest to e. g. `.repo/local_manifests/mintwrp-extended.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>

  <remote name="mintwrpext"
          fetch="https://github.com/mintwrp-extended"
          revision="android-8.1" />
  
  <remove-project name="android_build" path="build/make" />
  <project name="android_build_make" path="build/make" remote="mintwrpext" />

  <remove-project name="android_bootable_recovery" path="bootable/recovery" />
  <project name="android_bootable_recovery" path="bootable/recovery" remote="mintwrpext" />

  <remove-project path="TeamWin/.repo/frameworks/base" name="android_frameworks_base" />
  <project path="TeamWin/.repo/frameworks/base" name="halogenOS/android_frameworks_base" remote="github" revision="XOS-8.1" clone-depth="1">
    <linkfile src="core/java/android/content" dest="frameworks/base/core/java/android/content" />
    <linkfile src="core/java/android/security" dest="frameworks/base/core/java/android/security" />
  </project>

  <remove-project name="android_system_core" path="system/core" />
  <project name="android_system_core" path="system/core" remote="mintwrpext" />

  <remove-project name="android_vendor_omni" path="vendor/omni" />
  <project name="android_vendor_omni" path="vendor/omni" remote="mintwrpext" />
</manifest>
```

**Add your device's local manifest**

I hope you know what this means.

**Sync**

```bash
repo sync -j8 --force-sync -c -f --no-clone-bundle --no-tags
```

**Build**

```bash
lunch omni_<device>-userdebug
ALLOW_MISSING_DEPENDENCIES=true mka -j8 recoveryimage
```

### Stuff you get by using Minimal TWRP Extended

 - Capability of building kernel using Clang
 - Updated Lineage build additions
 - Shortened build fingerprint length
 - FBE support (install_keyring patch)
 - Keymaster V1 support
 - Support for synthetic password decryption (FBE on 8.1 for non-weaver devices)
 - New stuff from Omnirom gerrit
 - Miscellaneous fixes
