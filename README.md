### What is it?

A Vagrant configuration that starts up the PostgreSQL databases required
by [tDAR] in a virtual machine for local application development.

Based on this most excellent [code](https://github.com/jackdb/pg-app-dev-vm) and
[article](https://wiki.postgresql.org/wiki/PostgreSQL_For_Development_With_Vagrant) 

### Installation

First install [Vagrant] and [Virtual Box].

Then, run the following to create a new PostgreSQL app dev virtual machine:

	# Clone it locally:
    $ git clone https://github.com/MartinPaulo/pg-app-dev-vm TdarDbVm

    # Enter the cloned directory:
    $ cd TdarDbVm

    # Delete the old .git and README:
    $ rm -rf README.md .git

### Usage

    # Start up the virtual machine:
    $ vagrant up

    # Stop the virtual machine:
    $ vagrant halt

### What does it do?

It creates a virtual server running Ubuntu 12.04 with the latest version of 
PostgreSQL (*as of writing 9.3*) installed. It also edits the PostgreSQL 
configuration files to allow network access and creates the databases and users 
required to run tDAR.

Once it has started up it will print out how to access one of the the databases 
on the virtual machine. It will look something like this:

    $ vagrant up
    Bringing machine 'default' up with 'virtualbox' provider...
    [... truncated ...]
    Your PostgreSQL database has been setup and can be accessed on your local machine on the forwarded port (default: 15432)
      Host: localhost
      Port: 15432
      Database: tdardata
      Username: tdar
      Password: tdar

    Admin access to postgres user via VM:
      vagrant ssh
      sudo su - postgres

    psql access to app database user via VM:
      vagrant ssh
      sudo su - postgres
      PGUSER=myapp PGPASSWORD=dbpass psql -h localhost myapp

    Env variable for application development:
      DATABASE_URL=postgresql://myapp:dbpass@localhost:15432/myapp

    Local command to access the database via psql:
      PGUSER=myapp PGPASSWORD=dbpass psql -h localhost -p 15432 myapp

### License

This is released under the MIT license. See the file [LICENSE](LICENSE).

[tDAR]: http://www.tdar.org/
[Virtual Box]: https://www.virtualbox.org/
[Vagrant]: http://www.vagrantup.com/