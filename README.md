The Scala Library Installer Package for Android
===============================================

This is a distribution of the scala-library.jar for Android. It is meant for developers who want to use Scala in their
Android projects but don't want to redex and repackage Scala all the time while developing.

This installer package, instead, comes with the Scala library already pre-dex'd and splitted into Android-digestable hunks and
installs all parts of the library as a well-known Android framework library which you can use like e.g. the Google Maps library
which is pre-installed with Android.

Disclaimer
----------

Beware: The installer will change your system image and execute commands as root. I never managed to brick my phone this
way (which is highly unlikely) but don't say I didn't warn you. You use this program at your own risk.

Installation
------------

Just [download][apk] the apk and install it on your rooted phone / emulator and follow the instructions. In the process
the program will try to execute several commands with 'su' so this has to be enabled for your Android distribution.

To use the Scala library in one of your projects, add the following lines inside of the `<application>`-tag in the
`AndroidManifest.xml`:

        <uses-library android:name="scala.library" android:required="true"/>
        <uses-library android:name="scala.collection" android:required="true"/>
        <uses-library android:name="scala.collection.mutable" android:required="true"/>
        <uses-library android:name="scala.collection.immutable" android:required="true"/>
        <uses-library android:name="scala.collection.parallel" android:required="true"/>

You have to restart your phone afterwards or at least kill the `servicemanager` process. This will dexopt and cache the
newly added libraries.

What this is not
----------------
A way to distribute the Scala library to the users of your app. They will neither have this package installed nor will
they be able to because this works only on rooted phones. Remember to remove the `uses-library` from your AndroidManifest.xml
for production releases.


How does it work
----------------

Well-known libraries are declared in `/system/etc/permissions`. This installer extracts the Scala library onto your phone
and creates [descriptors][desc] in `/system/etc/permissions` which point to the installation location.

If it doesn't work
------------------

[Please file a bug][issues].

Credits
-------

[Stephane Micheloud][micheloud] already did much work on how to prepare an emulator image or a rooted phone to have Scala installed.
The process involved creating dex'd versions of the Scala library, a new image and adapting shell scripts.

  [micheloud]: http://lamp.epfl.ch/~michelou/android/index.html
  [apk]: http://blub.de
  [desc]: http://github.com/jrudolph/scala-android-libs/blob/master/src/main/res/raw/scala_collection_desc.xml
  [issues]: http://github.com/jrudolph/scala-android-libs/issues