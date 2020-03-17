## Change Log Stitch SDK

### 1.6.0 - 2020-03-16
 - Support AndroidX

### 1.5.3 - 2019-12-17
 - Fix download bug (update common framework)

### 1.5.2 - 2019-12-11
- Enable SSL TLS 1.2 by default for Android 4.4 and lower

### 1.5.1 - 2019-11-05
- Fix for RichText widget

### 1.5.0 - 2019-10-18
- Implement RichText widget

### 1.4.1 - 2019-08-14
- Disable Rakuten Analytics
- Remove Stitch-aquafadas module

### 1.4.0 - 2019-08-12
- Remove V1 from base endpoint 

### 1.3.5 - 2019-08-05
- In StitchKit replace Application by Context
- Update fresco version from 1.10.0 to 1.12.0 for REM 

### 1.3.4 - 2019-07-24
- Ignore web widget when url is empty
- Ignore unkown Widget sent from Stitch Editor (like richText)
- Fix : Video widget not parsed when Stitch is integrated in NextGen

### 1.3.3 - 2019-07-23
- Handle the new model returned by the Stitch api

### 1.3.2 - 2019-07-19
- Target common sdk 1.2.2
- Target gson 2.8.2 and support 28.0.0


### 1.3.1 - 2019-06-17
- Clean code
- Target SDK 1.1.+

### 1.3.0 - 2019-02-19
- Update target sdk to 28


### 1.2.1 - 18/09/2018

- Video in new window feature

### 1.2.0 - 10/09/2018

- Replace old video player by `Exoplayer` for video in banner
- Get default stitch for an app.


### 1.1.0 - 08/14/2018

- Continuous Integration.
- Testing - stitch-domain code MUST cover at least 80% of instructions with unit tests.
- User can specify custom end points for stitch api and kyashu.
- Improve documentation format published on REM doc -> Rename module `stitch` into `stitch-aquafadas` and `stitch-rakuten` into `stitch`.

### 1.0.0 - 06/22/2018
- Publishing first version of StitchSDK
