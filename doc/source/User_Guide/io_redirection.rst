.. raw:: latex

   \clearpage

.. _io:

I/O Redirection
===============

Rayleigh writes all text output (e.g., error messages, iteration
counter, etc.) to stdout by default. Different computing centers handle
stdout in different ways, but typically one of two path is taken. On
some machines, a log file is created immediately and updated
continuously as the simulation runs. On other machines, stdout is
buffered on-node and written to disk only when the run has terminated.

There are situations where it can be advantageous to have a regularly
updated log file whose update frequency may be controlled. This feature
exists in Rayleigh and may be accessed by assigning values to
**stdout_flush_interval** and **stdout_file** in the io controls
namelist.

::

   &io_controls_namelist
   stdout_flush_interval = 1000
   stdout_file = `routput'
   /

Set stdout_file to the name of a file that will contain Rayleigh’s text
output. In the example above, a file named *routput* will be appear in
the simulation directory and will be updated periodically throughout the
run. The variable stdout_flush_interval determines how many lines of
text are buffered before they are flushed to routput. Rayleigh prints
time-step information during each time step, and so setting this
variable to a relatively large number (e.g., 100+) prevents excessive
disk access from occurring throughout the run. In the example above, a
text buffer flush will occur once 1000 lines of text have been
accumulated.

Changes in the time-step size and self-termination of the run will also
force a text-buffer flush. Unexpected crashes and sudden termination by
the system job scheduler do not force a buffer flush. Note that the
default value of stdout_file is **‘nofile’**. If this value is
specified, output will directed to normal stdout.
