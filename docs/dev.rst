**************
Under The Hood
**************

This page contains information about the architecture of the driver and different techniques used for its development.

Automatic Code Generation
=========================

TBA

Threading Model
===============

TBA

Publishing States
=================

TBA

.. _sec-dev-dyn:

Configuring the Drone
=====================

TBA

.. _sec-dev-test:

Tests
=====

Upgrading Bebop SDK
===================

1. Update ``GIT_TAG`` of ``ARDroneSDK3`` in ``bebop_driver/CMakeLists.txt::ExternalProject_Add`` to your desired commit hash, branch or tag (release). The official upstream repository is hosted `here <https://github.com/ARDroneSDK3/ARSDKBuildUtils.git>`_.
2. Checkout (or browse) the upstream repository at the same hash used in step (1) and open ``repos.xml`` file. From this file, extract the commit hash of ``libARCommands`` from ``rev`` property of this XML tag: ``<repo name="libARCommands" rev="" />``.
3. Open ``bebop_driver/scripts/meta/generate.py`` and update ``LIBARCOMMANDS_GIT_HASH`` variable to the hash obtained in step (2).
4. Change the working diretory to ``bebop_driver/scripts/meta``, then execute ``generate.py`` from command line. This will regenerate all automatically generated message definitions, header files and documentations.
5. Copy the generated files to their target locations by calling ``install.sh``.
6. In ``bebop_driver/include/bebop_driver/autogenerated/ardrone3_setting_callbacks.h`` change ``ARCONTROLLER_DICTIONARY_KEY_ARDRONE3_PILOTINGSETTINGSSTATE_MAXDISTANCECHANGED_VALUE`` to ``ARCONTROLLER_DICTIONARY_KEY_ARDRONE3_PILOTINGSETTINGSSTATE_MAXDISTANCECHANGED_CURRENT``. This is due to a bug in upstream XML definitions.
7. Remove ``build`` and ``devel`` space of your ``catkin`` workspace, then re-build it.
