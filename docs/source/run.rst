.. _stginga-run:

Running Ginga With stginga Plugins
==================================

``stginga`` includes additional plugins to beyond those provided by Ginga
itself that add functionality.  There are a few different ways to start
Ginga in a way that will make it recognize those plugins; Only use *one* of the
following options:

#. :ref:`stginga-run-script`
#. :ref:`stginga-run-gingaconfig`
#. :ref:`stginga-run-manual`


.. _stginga-run-script:

The stginga Script
------------------

The simplest way is to simply use a script packaged with ``stginga`` that knows
how to preload the :ref:`STScI plugins <stginga-plugins>`. Note that this
currently only works when Ginga is run with the Qt backend::

    stginga [args]

The accepted command line arguments are the same as for standard Ginga,
with the following exceptions:

* There is no need to use ``--plugins`` and ``--modules`` to load STScI plugins.
* Toolkit (``--toolkit`` or ``-t``) is always set to Qt.


.. _stginga-run-gingaconfig:

Change Ginga Configuration to Always Load stginga
-------------------------------------------------

If you wish to have the ``stginga`` plugins *always* loaded when you
start Ginga, you can set your local configuration to do this automatically.
The key is to use Ginga's built-in configuration machinery.

Create a ``$HOME/.ginga/ginga_config.py`` file or modify your existing copy
with the following contents::

    def post_gui_config(ginga):
        from stginga import load_plugins
        load_plugins(ginga)

Then, you can run Ginga natively as follows::

    ginga [args]

Depending on how your system is set up, you might need to specify the toolkit,
because ``stginga`` plugins are currently only available for Qt::

    ginga --toolkit=qt [args]


.. _stginga-run-manual:

Manually Load stginga Plugins
-----------------------------

You can also run Ginga natively and just specify the plugins you want directly::

    ginga --plugins=stginga.plugins.BackgroundSub,stginga.plugins.DQInspect,stginga.plugins.MIPick,stginga.plugins.MultiImage [args]

As in :ref:`stginga-run-gingaconfig`, Qt toolkit is required.
