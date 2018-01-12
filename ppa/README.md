ppa instructions
================

Mail-in-a-Box maintains a Launchpad.net PPA ([Mail-in-a-Box PPA](https://launchpad.net/~mail-in-a-box/+archive/ubuntu/ppa)) for additional deb's that we want to have installed on systems.

Packages
--------

* postgrey, a fork of [postgrey](http://postgrey.schweikert.ch/) based on the [latest Debian package](http://git.debian.org/?p=collab-maint/postgrey.git), with a modification to whitelist senders that are whitelisted by [dnswl.org](https://www.dnswl.org/) (i.e. don't greylist mail from known good senders).

* dovecot-lucene, [dovecot's lucene full text search plugin](http://wiki2.dovecot.org/Plugins/FTS/Lucene), which isn't built by Ubuntu's dovecot package maintainer unfortunately.

Building
--------

To rebuild the packages in the PPA, you'll need to be @JoshData.

First:

* You should have an account on Launchpad.net.
* Your account should have your GPG key set (to the fingerprint of a GPG key on your system matching the identity at the top of the debian/changelog files).
* You should have write permission to the PPA.

To build:

	# Start a clean VM.
	vagrant up

	# Put your signing keys (on the host machine) into the VM (so it can sign the debs).
	gpg --export-secret-keys | vagrant ssh -- gpg --import

	# Build & upload to launchpad.
	vagrant ssh -- "cd /vagrant && make"

Mail-in-a-Box adds our PPA during setup, but if you need to do that yourself for testing:

	apt-add-repository ppa:mail-in-a-box/ppa
	apt-get update
	apt-get install postgrey dovecot-lucene

