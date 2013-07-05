tiopatinhas
===========

tiopatinhas is a companion for AWS's Auto Scaling. It attaches itself to an
Availability Group and adds resources bought in Amazon's Spot market.

As we can lose those instances at any time (due to market conditions),
tiopatinhas only allows itself to provide about 50% of the total number of
running instances.

Other features include:

* efficient use of resources. tiopatinhas is aware of Amazon's one-hour
billing cycles and has protections against "flapping"
* crash recovery: in case there is a market crash, tiopatinhas can acquire
instances on the regular OnDemand market
* fail-safe design: tiopatinhas fails "up". If the process crashes, the worse
thing that can happen is extra servers being left in the cluster. Amazon's
Autoscaling rules are not modified at all and can take over at any time.

Our theory of operations is that even when the system is live, each server is
actually about 50% idle so that the system can responde to changes in access
patterns. How much you can commit to Spot Instances is correlated to how low you
keep your load during normal system operations. Needless to say, you shouldn't
use Spot Instances in systems which are not fault tolerant.

Copy the template conf file (tp.conf.template) to tp.conf so that the script
can read it and make the changes according to your needs.

Also, you need to add a script on startup and shutdown to use the information on your user data to create the proper name and attach/dettach the instance to the load balancer, but that is up to you :)
