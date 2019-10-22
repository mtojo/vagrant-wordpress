# vagrant-wordpress

Local testing environment for WordPress.

## Prerequisites

The host you are using to run the local testing environment should have the following prerequisites:

* Install VirtualBox 5.1 or greater
* Install Vagrant 2.2.3 or greater

## Usage

### Run virtual server

```shell
$ vagrant up
$ vagrant reload
```

Open your browser at [http://192.168.33.10](http://192.168.33.10).

### Setup WordPress

In your browser, follow the steps outlined by the configuration process. Begin by reviewing the informational page and clicking the "Let's go!" button. Fill the database credentials as following:

* Database Name: `wordpress`
* Username: `root`
* Password: (empty)
* Database Host: `localhost`
* Table Prefix: `wp_`

Finally, select "Run the install" and supply the required values as prompted.

### Access phpMyAdmin

Open your browser at [http://192.168.33.10/phpmyadmin](http://192.168.33.10/phpmyadmin).

Login with the username `root` and an empty password.

### Stop virtual server

```shell
$ vagrant halt
```

## License

MIT
