Configuring I2P Zero Router Families
====================================

What is i2p-zero?
-----------------

Thanks to the hard work of the knaccc and the Monero community, i2p-zero
is a standalone version of the Java I2P router which comes bundled with
everything it needs to run, but no applications other than I2P Tunnel 
management and the SAM API. This can make it a great choice for people who
want to use I2P for a few specific applications, or host a web site on a
remote Virtual Private Server, or simply run a minimal, headless router
in order to donate bandwidth to the network. Perhaps the most exciting thing
about it though, is the opportunity it presents to incorporate I2P's privacy
featues into non-Java applications. [i2p-zero is a really cool project, and I
highly encourage you to check them out](https://github.com/i2p-zero/i2p-zero). 

What are Router Families and Why we Should/When we should not Use Them
----------------------------------------------------------------------

Router families are groups of I2P routers which cryptographically declare
that they belong to the same entity. The network can use this information
to help determine whether or not a sybil attack is occurring. If you are
running multiple high-bandwidth I2P routers, especially if they are primarily
used to donate bandwidth to the network, then you should declare that they
are part of the same router family.

If linking multiple routers to the same group of operators is a risk for you,
then you should not configure a router family.

Router Family Configuration
---------------------------

In order to configure i2p-zero to use a router family, you will need to
generate and copy router family key from an appliation which can create them.
In this example, we will use Java I2P to generate the family key.

### Step One: Generate and Export Router Family Keys

In order to generate a router family with Java I2P, go to the
[Configure Router Family(http://localhost:7657/configfamily)](http://localhost:7657/configfamily)
page. If you are not part of a router family, creating one will be the first
option on the list:

 - ![Generate a router family key](genfamilykey.png)

Simply click the button and a router family key will be generated for you in a
moment. After you generate the router family key, you will need to copy it so you
can use it with your i2p-zero routers. It will be located in your I2P keystore
directory(On Linux, this will usually be either `$HOME/.i2p/keystore` or 
`/var/lib/i2p/i2p-config/keystore`. The file will be named `yourfamily.ks`

### Step Two: Copy Router Family Information from `router.config` File

When you import a router family key to a Java I2P router, it writes a few
lines to it's configuration files to tell it what family it belongs to and where
to look for the router family keys. You will need to add these lines to your i2p-zero
configuration by hand. Look for them in the text field on the
[Advanced Configuration(http://localhost:7657/configadvanced)](http://localhost:7657/configadvanced)
page, they should start with `netdb.family,` and the only one you need is the `netdb.family.name`

        netdb.family.name=familyname

 - ![Find the family key properties](advfamilykey.png)

### Step Threee: Copy family key to i2p-zero base directory

Once you have a copy of your keystore and your key information, you can manually
import it into i2p-zero. First, take the keystore you located in step one, and
copy it to your i2p-zero configuration keystore directory. On Linux, this will
usually be `$HOME/.i2p-zero/config/keystore`, which you will probably need to create.
Copy the `yourfamily.ks` into the i2p-zero `config/keystore` directory.

### Step Four: Alter i2p-zero `router.config` file

Finally, add the `netdb.family.name=familyname` to your i2p-zero `router.config` file.
this will also be located in `$HOME/.i2p-zero/config`. When you restart your router, you
should become part of the router family.


