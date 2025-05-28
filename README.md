# How to edit elements in APK file 100% CAN RUN
### The example app to tutorial: Fancade.
# Need to prepare:
1. APKTool
2. Java JDK
3. Keytool + jarsigner (available in **JDK**)
4. New element to edit in your APK
5. APK Signature Tool (**apksigner** or **jarsigner**)
> Note: APKSigner is available in Android SDK.
# Now, get started!
🧩 **Step 1**: Extract APK using APKTool


``` 
apktool d fancade.apk -o fancade_src
 ```


> Note: Can use **7Zip** to extract!
🛠 **Step 2**: Edit your elements


> Do it **manually**: Go to the `fancade_src/assets/` or `res/raw/` folder, replace the audio file with the same name and format.


📦 **Step 3**: Repackage the APK


```
apktool b fancade1.0_src -o fancade_new_unsigned.apk
```


> Note: If you using **7ZIP** to extract, you can **compress to .ZIP** and then **rename to .APK**.
🔐 **Step 4** Create keystore mykey.keystore


``` 
keytool -genkey -v -keystore mykey.keystore -alias myalias -keyalg RSA -keysize 2048 -validity 10000
```


📌 **Parameter explanation**:


-keystore mykey.keystore: the name of the keystore file you want to create


-alias myalias: the alias name you use when signing


-keyalg RSA: encryption algorithm


-keysize 2048: key length


-validity 10000: number of days the key is valid (about ~27 years)


📝 **When running the command, you will be asked to enter**:


-Password for the keystore


-Name, organization, country,...


-Password for the alias (can be the same as the keystore password)


>❗ Remember the password carefully - if you **lose** it, you will **not** be able to sign APKs with that keystore anymore. The **only way** is: delete your old key and create a new one.


🔐 **Step 5**: Sign the APK with keystore mykey.keystore


*Method 1*: Use jarsigner (older)


```
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore mykey.keystore fancade_new_unsigned.apk myalias
```


> The signed APK is still **fancade_new_unsigned.apk**


*Method 2*: Use apksigner (recommended)


``` 
apksigner sign --ks mykey.keystore --out fancade_new.apk fancade_new_unsigned.apk
 ```


> Note: if CMD doesn't find APKSigner, use the command:


``` 
"C:\Users\<your-username>\AppData\Local\Android\Sdk\build-tools\36.0.0\apksigner.bat" sign --ks mykey.keystore --out fancade_new.apk fancade_new_unsigned.apk
```


> Note: edit "your-username".


# And now your APK is ready! Thank you for reading my page. Hope this helps!
