# php redirect
```text-x-php
<?php
    }

    if ( $return && !( strpos( $return, 'com_registration' ) || strpos( $return, 'com_login' ) ) ) {
    // checks for the presence of a return url
    // and ensures that this url is not the registration or login pages
        // If a sessioncookie exists, redirect to the given page. Otherwise, take an extra round for a cookiecheck
        if (isset( $_COOKIE[mosMainFrame::sessionCookieName()] )) {
            mosRedirect( $return );
        } else {
            mosRedirect( $mosConfig_live_site .'/index.php?option=cookiecheck&return=' . urlencode( $return ) );
        }
    } else {
        // If a sessioncookie exists, redirect to the start page. Otherwise, take an extra round for a cookiecheck
        if (isset( $_COOKIE[mosMainFrame::sessionCookieName()] )) {
            mosRedirect( $mosConfig_live_site .'/index.php' );
        } else {
            mosRedirect( $mosConfig_live_site .'/index.php?option=cookiecheck&return=' . urlencode( $mosConfig_live_site .'/index.php' ) );
        }
    }

} else if ($option == 'logout') {
    $mainframe->logout();

    // JS Popup message
    if ( $message ) {
        ?>
```