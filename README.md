## IDE 50
NOTE THESE COMMANDS WILL LIKELY NOT WORK


### Rolling a new version of appliance50 deb
1. `cd ~/ide50/ide50-2015/files`
2. Make desired changes. Be sure to ovewrite `/etc/ide50` with the new version
3. Use your favorite text editor to add a new changelog entry to
4. `~/ide50/ide50-2015/debian/changelog`
5. If you'd like to chmod stuff, do so in `~/ide50/ide50-2015/debian/postinst` after jharvard user is created
6. Now make the local deb with
7. `cd ~/ide50/ && make deb`
8. New deb can be found at `~/ide50/build/deb/` At this point if you'd like to test the deb in your machine before pushing to mirror you can do `sudo dpkg -i ide50-2015-*.deb`

### Pushing deb to mirror
1. Assuming deb was already built via the steps above do
2. `cd ~/ide50/build/deb`
3. `scp ide50_2015-*.deb user@local.cdn.cs50.net:~ # copy the deb to mirror`
4. `ssh user@local.cdn.cs50.net`
5. `sudo su rbowden # rbowden has the script to update the deb in mirror`
6. `cp ide50_2015-*.deb /home/rbowden # copy the deb to rbowden's home folder`
7. Finally execute the script that effectively uploads all debs in rbowden's home folder to production
8. `sudo /home/rbowden/deb/deb.sh`
9. At this point it's a good idea to test `sudo apt-get update` in the appliance to make sure everything works. Also, logs and errors generated by update50 can be found at `/var/log/ide50.log`

