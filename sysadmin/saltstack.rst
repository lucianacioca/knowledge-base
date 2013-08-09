
SaltStack
=========

Useful URL
----------

- `Salt Stack Walkthrough <http://docs.saltstack.com/topics/tutorials/walkthrough.html>`_
- `Pillar Walkthrough <http://docs.saltstack.com/topics/tutorials/pillar.html>`_
- `States tutorial, part 1 <http://docs.saltstack.com/topics/tutorials/states_pt1.html>`_
- `How Do I Use Salt States ? <http://docs.saltstack.com/topics/tutorials/starting_states.html>`_
- `Jinja2 documentation <http://jinja.pocoo.org/docs/>`_
- `[T] States tutorial, part 2 <http://docs.saltstack.com/topics/tutorials/states_pt2.html>`_
- `[T] State Enforcement <http://docs.saltstack.com/ref/states/index.html>`_

Useful Salt functions
---------------------

==================== ==========================================================
Function             Description
==================== ==========================================================
cmd.run              Execute command
network.interfaces   Dump network configuration
pillar.items         List pillars on minion
service.get_all      List all system services
state.highstate      Run all states
sys.doc              Show all available functions
test.ping            Test connectivity
==================== ==========================================================

One-liners
----------

Execute state :

    salt host1 state.sls utils.vim

How-to deploy a development environment
---------------------------------------

Requisite : Debian 7.0

Clone GIT repository :

	cd ~/git/
	git clone git://github.com/saltstack/salt.git

