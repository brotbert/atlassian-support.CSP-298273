# Atlassian Support Ticket CSP-298273

See [CSP-298273](https://getsupport.atlassian.com/servicedesk/customer/portal/14/CSP-298273)

## Setup vagrant box

Using [Vagrantfile](./Vagrantfile) we build a VM to reproduce the issue:

```
vagrant up
```

## Login to VM

Switch to GUI in VirtualBox and login.

* Credentials: vagrant/vagrant

You can change the screen size by navigating to [Display Settings](https://help.ubuntu.com/stable/ubuntu-help/look-resolution.html.en).

## Start Confluence

Open Terminal and run

```
atlas-run-standalone --product confluence --version 7.13.2
```

Wait until you see the message

```
Confluence started successfully in ... at http://localhost:1990
```

## Login to Confluence

Login to Confluence with [http://localhost:1990](http://localhost:1990)

* Credentials: admin/admin

## Upload document

Create a personal space and upload the document [Lorem Ipsum.docx](assets/Lorem%20Ipsum.docx).

## Preview the document

Preview the document:

![Lorem Ipsum.docx](screenshots/CSP-298273_default_1639320725552_28120__Running_-5.png#thumbnail)
