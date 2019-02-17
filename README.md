# Snappy nfs server

This snap contains nfs server which allows to export filesystems in the local network to use it in 
ubuntu core, server or desktop.

## Install

For now the snap is under development so is not available in the store yet. You can download git code 
and create the snap using snapcraft:

    $ git clone https://github.com/jmirasb/nfs-server-snap.git
    $ cd nfs-server-snap
    $ snapcraft

or download directly the snap in release section and install using snap:

    $ sudo snap install <snap> --dangerous --devmode

## Configure

The exports file is located in /var/snap/nfs-server/common/config and you can export directories directly editing the file or using:

    $ echo "/media/MYDRIVE  1.0.0.*(sync,no_subtree_check)" >>/var/snap/nfs-server/common/config/exports
    $ systemctl restart snap.nfs-server.nfsdaemon.service
  
and stop the exports using:

    $ systemctl stop snap.nfs-server.nfsdaemon.service

Visit http://nfs.sourceforge.net/nfs-howto/ar01s03.html for more information and configuration options.

You may announce exported filesystems using avahi snap. You just need to create the appropriate service in the avahi config directory (/var/snap/avahi/common/etc/avahi/services):

     $ <?xml version="1.0" standalone='no'?>
     $ <!DOCTYPE service-group SYSTEM "avahi-service.dtd">
     $ <service-group>
     $ <name replace-wildcards="yes">MYDRIVE shared in %h</name>
     $ <service>
     $ <type>_nfs._tcp</type>
     $ <port>2049</port>
     $ <txt-record>path=/media/MYDRIVE</txt-record>
     $ </service>
     $ </service-group>

If you announce the nfs export you must add "insecure" in the export option.

## Issues

Please report the snap issues to project issues section.
