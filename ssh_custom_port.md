# Change SSH

# ssh to router
# create /etc/dropbear/authorized_keys
# add ssh public key

chmod 700 /etc/dropbear
chmod 600 /etc/dropbear/authorized_keys

# test ssh to router, it should login without asking password

# configure /etc/config/firewall
config rule
        option name             Allow-SSH
        option src              wan
        option proto            tcp
        option dest_port        2200
        option target           ACCEPT

# restart Firewall
/etc/init.d/firewall restart

# change passwork to strong one
passwd root

# configure /etc/config/dropbear
config dropbear
        option PasswordAuth 'off'
        option RootPasswordAuth 'off'
        option Port         '2200'

# reload dropbear
/etc/init.d/dropbear reload

# check connection
ssh router -p 2200

