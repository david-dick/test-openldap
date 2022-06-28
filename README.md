# NAME

Test::OpenLDAP - Creates a temporary instance of OpenLDAP's slapd daemon to run tests against.

# VERSION

Version 0.71

# SYNOPSIS

    my $slapd = Test::OpenLDAP->new(); # Test::OpenLDAP->new( suffix => 'dc=foobar,dc=com', 'debug' => '-1' );

    my $ldap = Net::LDAP->new($slapd->uri()) or Carp::croak("Failed to connect:$@");

    my $mesg = $ldap->bind($slapd->admin_user(), password => $slapd->admin_password());

    ... add / modify / search entries

    $slapd->stop();

    $slapd->start();

    $slapd->DESTROY();

# DESCRIPTION

This module allows easy creation and tear down of a OpenLDAP slapd instance.  When the variable goes 
out of scope, the slapd instance is torn down and the file system objects it relies on are removed.

# SUBROUTINES/METHODS

## new

This method initialises and starts an OpenLDAP slapd instance, listening on a unix socket.  It then creates an admin user and password and returns the slapd instance to the user.
The method accepts a hash of configuration options.  The following keys are currently accepted;

- suffix - specifies the suffix that subsequent LDAP queries will be procesed under (e.g. 'dc=example,dc=org')
- debug - the debug level of the slapd instance.  To see valid values for debug, execute the command "slapd -d '?'".  slapd will list all the valid debug levels. It defaults to '0' or no logging.
- syslog - the debug level of the slapd instance for syslog.  This parameter accepts the same values as the debug level.  It defaults to '0' or no logging to syslog

## skip

This method allows the user to skip tests requiring Test::OpenLDAP by checking to see if the slapd binary exists AND that the OS uses fork for process control.

## start

This methods starts the slapd process 

## start

This method stops the slapd process 

## uri

This method gives the uri for the test code to connect to via a Net::LDAP->new() call.

## suffix

This method gives the dn used as the suffix for the slapd database.

## admin\_user

This method gives the admin user name for the slapd database.

## admin\_password

This method gives the admin password for the slapd database.

## debug 

This method gives the debug level that the slapd instance is reporting.

## debug\_handle

This method gives a handle to the slapd debug log.

## set\_cookie

This method sets the value for the "-c" argument to slapd. This can be used to force a reload for a replication consumer.

## get\_cookie

This method gets the value for the "-c" argument to slapd.

## clear\_cookie

This method clears the value for the "-c" argument to slapd. This can be used to reset the cookie in between stopping and starting slapd

## new\_db\_directory

This method creates and returns a new database directory (for subsequent use with the olcDbDirectory attribute)

# DIAGNOSTICS

- `slapd already started`

    Each instance of Test::OpenLDAP may only start one instance of slapd at a time.

# CONFIGURATION AND ENVIRONMENT

Test::OpenLDAP requires no configuration files or environment variables.  

# DEPENDENCIES

Test::OpenLDAP requires the following non-core Perl modules

- [Data::UUID](https://metacpan.org/pod/Data::UUID)
- [File::Temp](https://metacpan.org/pod/File::Temp)
- [URI::Escape](https://metacpan.org/pod/URI::Escape)
- [Net::LDAP](https://metacpan.org/pod/Net::LDAP)

# INCOMPATIBILITIES

None reported

# AUTHOR

David Dick, `<ddick at cpan.org>`

# BUGS AND LIMITATIONS

Please report any bugs or feature requests to `bug-test-openldap at rt.cpan.org`, or through
the web interface at [http://rt.cpan.org/NoAuth/ReportBug.html?Queue=Test-OpenLDAP](http://rt.cpan.org/NoAuth/ReportBug.html?Queue=Test-OpenLDAP).  I will be notified, and then you'll
automatically be notified of progress on your bug as I make changes.

# SUPPORT

You can find documentation for this module with the perldoc command.

    perldoc Test::OpenLDAP

You can also look for information at:

- RT: CPAN's request tracker (report bugs here)

    [http://rt.cpan.org/NoAuth/Bugs.html?Dist=Test-OpenLDAP](http://rt.cpan.org/NoAuth/Bugs.html?Dist=Test-OpenLDAP)

- AnnoCPAN: Annotated CPAN documentation

    [http://annocpan.org/dist/Test-OpenLDAP](http://annocpan.org/dist/Test-OpenLDAP)

- CPAN Ratings

    [http://cpanratings.perl.org/d/Test-OpenLDAP](http://cpanratings.perl.org/d/Test-OpenLDAP)

- Search CPAN

    [http://search.cpan.org/dist/Test-OpenLDAP/](http://search.cpan.org/dist/Test-OpenLDAP/)

# LICENSE AND COPYRIGHT

Copyright 2017 David Dick.

This program is free software; you can redistribute it and/or modify it
under the terms of either: the GNU General Public License as published
by the Free Software Foundation; or the Artistic License.

See http://dev.perl.org/licenses/ for more information.
