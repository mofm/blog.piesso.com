.. title: Vim Tips: Channel
.. slug: vim-tips-channel
.. date: 2021-12-22 18:32:45 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

Vim supported channels for inter-process communication and job channels communicate with other processes.
Also, The vim packages contains the demo channel server(demoserver.py). You can find **demoserver.py** script in *"$VIMRUNTIME/tools/"*. *"$VIMRUNTIME"* path, may change according to your distro: 

My path, "/usr/share/vim/vim82/tools/demoserver.py" on Gentoo Linux. 

* First, run the demo server in a terminal.

.. code-block:: bash


  $ python /usr/share/vim/vim82/tools/demoserver.py


* And then, run Vim in another terminal. 

* For detailed information, I am quoting from the script::


  # Server that will accept connections from a Vim channel.
  # Run this server and then in Vim you can open the channel:
  #  :let handle = ch_open('localhost:8765')
  #
  # Then Vim can send requests to the server:
  #  :let response = ch_sendexpr(handle, 'hello!')
  #
  # And you can control Vim by typing a JSON message here, e.g.:
  #   ["ex","echo 'hi there'"]
  #
  # There is no prompt, just type a line and press Enter.
  # To exit cleanly type "quit<Enter>".
  #
  # See ":help channel-demo" in Vim.
  #
  # This requires Python 2.6 or later.

