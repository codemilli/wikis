The Esky must be given its location on disk, and a url at which to look for
updated versions. Instances of Esky then have the following useful methods:

 > app = esky.Esky(sys.executable,"http://example-app.com/downloads/")

app.version:                the current best available version.

    app.active_version:         the currently-executing version, or None
                                if the esky isn't for the current app.

    app.find_update():          find the best available update, or None
                                if no updates are available.

    app.fetch_version(v):       fetch the specified version into local storage.

    app.install_version(v):     install and activate the specified version.

    app.uninstall_version(v):   (try to) uninstall the specified version; will
                                fail if the version is currently in use.

    app.cleanup():              (try to) clean up various partly-installed
                                or old versions lying around the app dir.

    app.reinitialize():         re-initialize internal state after changing
                                the installed version.

    auto_update():   check for an updated version; install it if found


If updating an application that is not writable by normal users, esky has the
ability to gain root privileges through the use of a helper program.  The
following methods control this behaviour:

    app.has_root():             check whether esky currently has root privs.

    app.get_root():             escalate to root privs by spawning helper app.

    app.drop_root():            kill helper app and drop root privileges

