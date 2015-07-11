## Ports for constructing lxde

Contributions are welcome

### How to test this git:

#### 1. Clone it

    # git clone git://github.com/NuTyX/lxde.git

#### 2. adjust /etc/cards.conf by adding the ports directory. By default it should be:

      dir /var/lib/pkg/saravane/lxde


#### 3. Run the script a first time (in root)

    # bash lxde/scripts/lxde

This will populate all the directories 

#### 4. build the ports

##### 4.1 With the command "cards depcreate"
    # cards depcreate lxde


##### 4.2 With the command "cards create -r" 
This method means you have ALL the binaries of the base,console and graphic collection. You want to build like on the bot.

###### 4.2.1 build a list of package to build by running the script a second time

    # bash lxde/scritps/lxde|cut -d " " -f1 > list

###### 4.2.2 build each package per level

    # for i in `cat list`
    # do
    #   cards level|grep /$i$|grep  ^0:
    # done

It will print a list of package to be build from level 0, if not start do it again with next level

    # for i in `cat list`
    # do
    #  cards level|grep /$i$|grep  ^1:
    # done

and so on. Exemple for level 2:

    2: /lxde/lxde-libui

Time to build:

    # for i in lxde-libui
    # do
    #   cards create -r $i||break
    # done

It will break at the first failure

Have fun :)
